# Auto-Evaluation

## Introduction
Auto-Evaluation is a multi-chip adaptive model automatic evaluation tool built on the <a href="https://flageval.baai.ac.cn/#/home" target="_blank">  FlagEval </a> platform. It supports Embodied VLM models and is bound with ten classic datasets. Currently, it only supports online evaluation. This tool provides interfaces for starting evaluation, checking evaluation progress, viewing evaluation results, stopping evaluation, resuming evaluation, and analyzing differences in multi-chip evaluation results. Whether for individuals, teams, or enterprises, as long as the service is launched on compute resources and supports public network access, automatic evaluation can be performed using this tool.

## Tool Description
### 1. Tool Address:
120.92.17.239:5050
### 2. Tool Interface Introduction:

| **API Name** | **Method** | **Description** |
| --- | --- | --- |
| /evaluation | POST | Start evaluation; calls the uploaded service URL synchronously to begin model inference |
| /evaldiffs | GET | Query evaluation results |
| /stop_evaluation | POST | Stop evaluation; use this interface if the evaluation needs to be paused due to service issues |
| /resume_evaluation | POST | Resume evaluation; supports resuming from breakpoints |
| /evaluation_progress | POST | View evaluation progress; returns detailed information on completed datasets |
| /evaluation_diffs | POST | View result differences between multiple models |

## Detailed Interface Parameter Description

### 1. Start Evaluation

#### Request Interface

##### header
    ```json
    "Content-Type": "application/json" 
    ```
##### body:

| Parameter Name | Type | Description | Required |
| --- | --- | --- | --- |
| eval_infos | EvalInfo[] | List of model evaluation service info | Yes |
| domain | string | Evaluation Domain: MM | Yes |
| mode | string | Evaluation Project ID: EmbodiedVerse | No |
| region | string | Evaluation Tool Cluster: bj (default), sz | No |
| special_event | string | Whether it is a chip evaluation, default is yes | No |
| user_id | int | User ID on FlagEval platform | No |

EvalInfo Data Structure Parameters
| **Parameter Name** | **Type** | **Description** | **Required** |
|--------------------|----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------|
| eval_model         | string   | Name of the evaluation task to be started, must be unique (to clarify if the evaluation is an Nvidia baseline model, please name it using xxx-nvidia-origin)                                                     | Yes          |
| model              | string   | The model used when deployed as a service (multiple evaluations started with the same model will use the same cache). Note: If using RoboBrain2.0 series models, please include RoboBrain2.0 in the name.      | Yes          |
| eval_url           | string   | Evaluation interface for each model deployment service, eg: [http://10.1.15.153:9010/v1/chat/completions](http://10.1.15.153:9010/v1/chat/completions)                                                                                                         | Yes          |
| tokenizer          | string   | Vendor and model information, eg: Qwen/Qwen3-8B                                                                                                                                                                 | Yes          |
| api_key            | string   | Model call API_KEY, default is "EMPTY"                                                                                                                                                                          | No           |
| batch_size         | int      | Batch_size enabled for the model, default is 1                                                                                                                                                                  | No           |
| num_concurrent     | int      | Number of concurrent requests, default is 1                                                                                                                                                                     | No           |
| num_retry          | int      | Number of retries, default is 10                                                                                                                                                                                | No           |
| gen_kwargs         | string   | Model emphasis parameters like temperature, topn, etc., separated by ","<br>eg: temperature=0.6,top_k=20,top_p=0.95,min_p=0<br>NLP uses max_gen_toks; for max_model_len of 16384, please set max_gen_toks=16000<br>MM, EV use the max_gen_toks field to specify | No           |
| thinking           | bool     | Whether to enable the thinking model, currently only applicable to EmbodiedVerse's RoboBrain, default is False                                                                                                  | No           |
| retry_time         | int      | Timeout duration, currently supports MM and Embodied domains<br>Current default is 3600s                                                                                                                        | No           |
| chip               | string   | Name of the chip used for evaluation, format: Vendor-Chip Name<br>Default is: Nvidia-H100                                                                                                                       | No           |
| base_model_name    | string   | Base model used for evaluation, eg: Qwen3-8B                                                                                                                                                                    | No           |

#### Response Data:

Note: As model evaluation takes a long time, the interface temporarily returns the corresponding evaluation ID and batch ID. Evaluation results can be queried later using this information.
| **Parameter Name** | **Type** | **Description** | **Required** |
|--------------------|----------|---------------------------------------------------------------------------------|--------------|
| err_code           | int      | Whether the request was processed correctly, 0 for success, 1 for failure; if 1, response data does not include request_id | Yes          |
| err_msg            | string   | Request processing message                                                      | Yes          |
| request_id         | string   | Unique Identifier                                                               | Yes          |
| eval_tasks         | EvalTask[]| Detailed information of evaluations started by each service                    | Yes          |

### 2. View Evaluation Results

#### Request Interface

##### header

    ```bash
    "Content-Type": "application/json" 
    ```

##### body:

| Parameter Name | Type | Description | Required |
| --- | --- | --- | --- |
| request_id | string | Unique Identifier | Yes |

#### Response Data

| Parameter Name | Type | Description | Required |
| --- | --- | --- | --- |
| err_code | int | Whether the request was processed correctly, 0 for success, 1 for failure | Yes |
| err_message | string | Request processing message | Yes |
| eval_results | EvalResultMap | Evaluation result information for each started service | Yes |

EvalResultMap Data Structure
| Parameter Name      | Type                   | Description                                  | Required |
|---------------------|------------------------|----------------------------------------------|----------|
| EvalResultMap       | Map<string, EvalResult>| Evaluation results for all models started in one batch | Yes      |
| EvalResultMap.key   | string                 | Corresponding eval_model of the started evaluation | Yes      |
| EvalResultMap.value | EvalResult[]           | Evaluation results for a single model        | Yes      |

EvalResult Data Structure
| Parameter Name | Type     | Description                                                                 | Required |
|----------------|----------|-----------------------------------------------------------------------------|----------|
| status         | string   | Evaluation status. eg: S: Success, F: Failure, C: Cancelled, OOR: Out of Retries | Yes      |
| details        | Detail[] | Evaluation results for each dataset of the corresponding service (currently only supports mmlu, gsm8k) | Yes      |
| release        | bool     | Whether the model can be released, if the diff is within acceptable range   | Yes      |

Detail Data Structure
| Parameter Name | Type   | Description                                            | Required |
|----------------|--------|--------------------------------------------------------|----------|
| dataset        | string | Dataset name                                           | Yes      |
| status         | string | Running status of the corresponding evaluation service, eg: S: Success, F: Failure, C: Cancelled | Yes      |
| accuracy       | float  | Dataset evaluation result                              | Yes      |
| diff           | float  | Difference between dataset evaluation result and Nvidia baseline | Yes      |

### 3. Stop Evaluation

#### Request Interface

##### header


    ```bash
    "Content-Type": "application/json" 
    ```



##### body:

| Parameter Name | Type | Description | Required |
| --- | --- | --- | --- |
| request_id | string | Unique Identifier | Yes |

#### Response Data

| Parameter Name | Type | Description | Required |
| --- | --- | --- | --- |
| err_code | int | Whether the request was processed correctly, 0 for success, 1 for failure | Yes |
| err_message | string | Request processing message | Yes |

### 4. Resume Evaluation

#### Request Interface

##### header

    ```bash
    "Content-Type": "application/json" 
    ```


##### body:

| Parameter Name | Type | Description | Required |
| --- | --- | --- | --- |
| request_id | string | Unique Identifier | Yes |

#### Response Data

| Parameter Name | Type | Description | Required |
| --- | --- | --- | --- |
| err_code | int | Whether the request was processed correctly, 0 for success, 1 for failure | Yes |
| err_message | string | Request processing message | Yes |

### 5. Query Evaluation Progress

#### Request Interface

##### header

    ```bash
    "Content-Type": "application/json" 
    ```


##### body:

| Parameter Name | Type | Description | Required |
| --- | --- | --- | --- |
| request_id | string | Unique Identifier | Yes |
| domain | string | Evaluation Domain (NLP, MM) | Yes |

#### Response Data

| **Parameter Name** | **Type** | **Description** | **Required** |
| --- | --- | --- | --- |
| err_code | int | Whether the request was processed correctly, 0 for success, 1 for failure | Yes |
| err_message | string | Request processing message | Yes |
| finished | bool | Whether the evaluation is finished | Yes |
| status | string | Evaluation status | Yes |
| datasets_progress | string | Dataset progress | Yes |
| running_dataset | string | Currently running dataset | Yes |
| running_progress | string | Evaluation progress within the running dataset | Yes |

### 6. Query Evaluation Differences

#### Request Interface

##### header

    ```bash
    "Content-Type": "application/json" 
    ```


##### body:

| Parameter Name | Type | Description | Required |
| --- | --- | --- | --- |
| request_ids | string[] | Unique Identifier | Yes |

#### Response Data

| **Parameter Name** | **Type** | **Description** | **Required** |
| --- | --- | --- | --- |
| err_code | int | Whether the request was processed correctly, 0 for success, 1 for failure | Yes |
| err_message | string | Request processing message | Yes |
| eval_diffs | EvalDiff[] | List of evaluation result comparisons | Yes |

EvalDiff Data Structure
| **Parameter Name** | **Type** | **Description** | **Required** |
|--------------------|----------|----------------------------------|--------------|
| request_id         | string   | UUID of the evaluated record     | Yes          |
| details            | Detail[] | Detailed comparison data for each dataset | Yes          |
| release            | bool     | Whether release conditions are met | Yes          |

Detail Data Structure
| **Parameter Name** | **Type** | **Description** | **Required** |
|--------------------|----------|------------------------------------------------|--------------|
| dataset            | string   | Dataset name                                   | Yes          |
| base_acc           | float    | Baseline score                                 | Yes          |
| accuracy           | float    | Evaluated dataset score                        | Yes          |
| diff               | float    | Difference between evaluated dataset and baseline dataset | Yes          |
