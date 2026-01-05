[中文](./README_cn.md)

## FlagOS-Robo Overview

🤖 FlagOS-Robo is built upon the unified and open-source AI system software stack, [FlagOS](https://flagos.io), which supports various AI chips.
It serves as an integrated training and inference framework for AI models used in robots🤖 , so-called Embodied Intelligence.
It can be deployed across diverse scenarios, ranging from edge to cloud.
Being portable across various chip models, it enables efficient training, inference, and deployment
for both Vision Language Models (VLMs) and Vision Language Action (VLA) models.
Here, VLMs usually act as the brain🧠 for task planning, while VLA models act as the cerebellum to output actions for robot control🦾.

FlagOS-Robo supports the full lifecycle of embodied intelligence models,
including **data loading** from diverse formats (webdataset, Megatron-Energon and lerobot dataset), **supervised fine-tuning** (SFT),
**inference deployment**, and integrated **testing and evaluation** via the [FlagEval-Robo](https://embodiedverse.flageval.net/home) platform. Users can easily reproduce the full end-to-end pipeline in their own environment by downloading and running the provided examples.

FlagOS-Robo has been deeply integrated into **BAAI’s Embodied Intelligence platform** [RoboXStudio](https://ei2data.baai.ac.cn/home), which provides one-stop services including real-robot data collection, data annotation, supervised fine-tuning of VLA models, and evaluation. Users without a local setup can directly access RoboXStudio and run experiments without any installation.

FlagOS-Robo provides a powerful computational foundation and systematic support for cutting-edge researches
and industrial applications in embodied intelligence, accelerating innovations and real-world deployments
of intelligent agents.

## Feature Highlights

- [FlagScale](https://github.com/flagos-ai/FlagScale/tree/main) as users' entrypoint supports robot related AI model training and inference, including Pi-0, RoboBrain2, and RoboBrainX0, etc.
- FlagOS-Robo supports [RoboOS](https://github.com/FlagOpen/RoboOS)-based cross-embodiment collaboration,
  ensuring compatibility with different data formats, efficient edge-cloud coordination,
  and real-machine evaluation.

## Quick Start🚀

### Installation
[Install](https://github.com/flagos-ai/FlagScale?tab=readme-ov-file#-setup) FlagScale.

### Train
[Train](https://github.com/flagos-ai/FlagScale?tab=readme-ov-file#train) models via FlagScale.

### Inference
Model [inference](https://github.com/flagos-ai/FlagScale/tree/main?tab=readme-ov-file#inference)  via FlagScale.

### Serve
[Serving](https://github.com/flagos-ai/FlagScale?tab=readme-ov-file#serve) models as a service via FlagScale.

### Evaluation
Evaluate(https://github.com/flagos-ai/FlagScale?tab=readme-ov-file#evaluation) models via FlagScale and [FlagEval](https://flageval.baai.ac.cn/#/home).


## Support Matrix
| Models | Type | Checkpoint | Train | Inference | Serve | Evaluate |
|--------------|--------|--------|--------|-------------------|----------------------|---------------------------|
| PI0 | VLA | [Huggingface](https://huggingface.co/lerobot/pi0_base) | ✅︎  [Guide](https://github.com/flagos-ai/FlagScale/blob/main/examples/pi0/README.md#training) | ✅︎  [Guide](https://github.com/flagos-ai/FlagScale/blob/main/examples/pi0/README.md#inference) | ✅ [Guide](https://github.com/flagos-ai/FlagScale/blob/main/examples/pi0/README.md#service) | ❌ |
| PI0.5 | VLA | [Huggingface]() | ✅︎  [Guide](https://github.com/flagos-ai/FlagScale/blob/main/examples/pi0_5/README.md#training) | ✅ [Guide](https://github.com/flagos-ai/FlagScale/blob/main/examples/pi0_5/README.md#inference) | ✅   [Guide](https://github.com/flagos-ai/FlagScale/blob/main/examples/pi0_5/README.md#serving)|  ❌ |
| RoboBrain-2.0 | VLM | [Huggingface]() | ✅︎  [Guide](https://github.com/flagos-ai/FlagScale/blob/main/flagscale/models/megatron/qwen2_5_vl/QuickStart.md) | ✅ | ✅ | ✅   [Guide](https://github.com/flagos-ai/FlagScale?tab=readme-ov-file#evaluation) |
| RoboBrain-X0 | VLA | [Huggingface]() | ✅︎  [Guide](https://github.com/flagos-ai/FlagScale/blob/main/examples/robobrain_x0/README.md#training) | ❌ | ✅   [Guide](https://github.com/flagos-ai/FlagScale/blob/main/examples/robobrain_x0/README.md#serving)| ❌ |
| RoboBrain-X0.5 | VLA | [Huggingface](https://github.com/flagos-ai/FlagScale/blob/main/examples/robobrain_x0_5/README.md#training) | ✅︎  [Guide]() | ❌ | ✅   [Guide](https://github.com/flagos-ai/FlagScale/blob/main/examples/robobrain_x0_5/README.md#serving)| ❌|
