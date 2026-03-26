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

| Models | Type | Checkpoint | Train | Inference | Serve | Evaluate |
|--------------|--------|--------|--------|-------------------|----------------------|---------------------------|
| PI0 | VLA | [Huggingface](https://huggingface.co/lerobot/pi0_base) | ✅︎  [Guide](https://github.com/flagos-ai/FlagScale/blob/main/examples/pi0/README.md#training) | ✅︎  [Guide](https://github.com/flagos-ai/FlagScale/blob/main/examples/pi0/README.md#inference) | ✅ [Guide](https://github.com/flagos-ai/FlagScale/blob/main/examples/pi0/README.md#serving) | ❌ |
| PI0.5 | VLA | [Huggingface](https://huggingface.co/lerobot/pi05_libero_base) | ✅︎  [Guide](https://github.com/flagos-ai/FlagScale/blob/main/examples/pi0_5/README.md#training) | ✅ [Guide](https://github.com/flagos-ai/FlagScale/blob/main/examples/pi0_5/README.md#inference) | ✅   [Guide](https://github.com/flagos-ai/FlagScale/blob/main/examples/pi0_5/README.md#serving)|  ❌ |
| RoboBrain-2.0 | VLM | [Huggingface](https://huggingface.co/BAAI/RoboBrain2.0-7B) | ✅︎  [Guide](https://github.com/flagos-ai/FlagScale/blob/main/examples/qwen2_5_vl/README.md) | ✅[Guide](https://github.com/flagos-ai/FlagScale/blob/main/examples/robobrain2/README.md#inference) | ✅[Guide](https://github.com/flagos-ai/FlagScale/blob/main/examples/robobrain2/README.md#serving) | ✅   [Guide](https://github.com/flagos-ai/FlagScale/blob/main/examples/qwen2_5_vl/README.md#evaluation) |
| RoboBrain-2.5 | VLM | [Huggingface](https://huggingface.co/collections/BAAI/robobrain25) | ✅︎  [Guide](https://github.com/flagos-ai/FlagScale/blob/main/examples/qwen3_vl/README.md) | ✅[Guide](https://github.com/flagos-ai/FlagScale/blob/main/examples/robobrain2_5/README.md#inference) | ✅[Guide](https://github.com/flagos-ai/FlagScale/blob/main/examples/robobrain2_5/README.md#serving) | ✅   [Guide](https://github.com/flagos-ai/FlagScale/blob/main/examples/qwen2_5_vl/README.md#evaluation) |
| RoboBrain-X0 | VLA | [Huggingface](https://huggingface.co/BAAI/RoboBrain-X0-Preview) | ✅︎  [Guide](https://github.com/flagos-ai/FlagScale/blob/main/examples/robobrain_x0/README.md#training) | ❌ | ✅   [Guide](https://github.com/flagos-ai/FlagScale/blob/main/examples/robobrain_x0/README.md#serving)| ❌ |
| Qwen-GR00T | VLA | [Huggingface](https://huggingface.co/Qwen/Qwen3-VL-4B-Instruct) | ✅︎  [Guide](https://github.com/flagos-ai/FlagScale/blob/main/examples/qwen_gr00t/README.md#training) | ✅ [Guide](https://github.com/flagos-ai/FlagScale/blob/main/examples/qwen_gr00t/README.md#inference) | ✅   [Guide](https://github.com/flagos-ai/FlagScale/blob/main/examples/qwen_gr00t/README.md#serving)| ✅   [Guide](https://github.com/flagos-ai/FlagScale/blob/main/examples/qwen_gr00t/README.md#evaluation) |
| GR00T-N1.5 | VLA | [Huggingface](https://huggingface.co/nvidia/GR00T-N1.5-3B) | ✅︎  [Guide](https://github.com/flagos-ai/FlagScale/tree/main/examples/gr00t_n1_5#training) | ❌ | ✅   [Guide](https://github.com/flagos-ai/FlagScale/tree/main/examples/gr00t_n1_5#serving)|  ❌ |