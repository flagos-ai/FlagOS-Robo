[English](./README.md)

## 介绍

FlagOS-Robo 基于开源开放的多芯片 AI 软件栈 [FlagOS](https://flagos.io) 构建，是一个面向具身智能的训练与推理一体化框架。
它支持从端到云的多场景部署，兼容多种芯片，能够同时实现大脑模型（VLM）与小脑模型（VLA）的高效协同训练与推理。
FlagOS-Robo 打通从数据采集到真机与评测平台（[FlagEval](https://github.com/FlagOpen/FlagEval/)）的全流程链路，
已深度集成于智源具身智能一站式平台。
通过这一完整生态，FlagOS-Robo 将为具身智能的前沿研究与产业应用提供强大的算力底座与系统化支撑，加速智能体技术的创新与落地。

## 核心特性

- 通过 FlagOS 软件栈实现具身智能大、小脑模型的跨芯片高效训练与推理，既支持不同云侧服务器芯片，又支持不同端侧模组。
- 实现大脑模型（VLM）和小脑模型（VLA）从训练与推理部署全流程所需功能，并提供用户简单易用接口，可自适应调优和一键部署。
- 支持 [RoboOS](https://github.com/FlagOpen/RoboOS) 跨本体协作，实现不同数据格式兼容、高效端云协同、真机评测等功能。


## 快速上手🚀

| 模型 | 类型 | 模型权重 | 训练 | 离线推理 | 在线推理 | 评估 |
|--------------|--------|--------|--------|-------------------|----------------------|---------------------------|
| PI0 | VLA | [Huggingface](https://huggingface.co/lerobot/pi0_base) | ✅︎  [Guide](https://github.com/flagos-ai/FlagScale/blob/main/examples/pi0/README.md#training) | ✅︎  [Guide](https://github.com/flagos-ai/FlagScale/blob/main/examples/pi0/README.md#inference) | ✅ [Guide](https://github.com/flagos-ai/FlagScale/blob/main/examples/pi0/README.md#serving) | ❌ |
| PI0.5 | VLA | [Huggingface](https://huggingface.co/lerobot/pi05_libero_base) | ✅︎  [Guide](https://github.com/flagos-ai/FlagScale/blob/main/examples/pi0_5/README.md#training) | ✅ [Guide](https://github.com/flagos-ai/FlagScale/blob/main/examples/pi0_5/README.md#inference) | ✅   [Guide](https://github.com/flagos-ai/FlagScale/blob/main/examples/pi0_5/README.md#serving)|  ❌ |
| RoboBrain-2.0 | VLM | [Huggingface](https://huggingface.co/BAAI/RoboBrain2.0-7B) | ✅︎  [Guide](https://github.com/flagos-ai/FlagScale/blob/main/examples/qwen2_5_vl/README.md) | ✅[Guide](https://github.com/flagos-ai/FlagScale/blob/main/examples/robobrain2/README.md#inference) | ✅[Guide](https://github.com/flagos-ai/FlagScale/blob/main/examples/robobrain2/README.md#serving) | ✅   [Guide](https://github.com/flagos-ai/FlagScale/blob/main/examples/qwen2_5_vl/README.md#evaluation) |
| RoboBrain-2.5 | VLM | [Huggingface](https://huggingface.co/collections/BAAI/robobrain25) | ✅︎  [Guide](https://github.com/flagos-ai/FlagScale/blob/main/examples/qwen3_vl/README.md) | ✅[Guide](https://github.com/flagos-ai/FlagScale/blob/main/examples/robobrain2_5/README.md#inference) | ✅[Guide](https://github.com/flagos-ai/FlagScale/blob/main/examples/robobrain2_5/README.md#serving) | ✅   [Guide](https://github.com/flagos-ai/FlagScale/blob/main/examples/qwen2_5_vl/README.md#evaluation) |
| RoboBrain-X0 | VLA | [Huggingface](https://huggingface.co/BAAI/RoboBrain-X0-Preview) | ✅︎  [Guide](https://github.com/flagos-ai/FlagScale/blob/main/examples/robobrain_x0/README.md#training) | ❌ | ✅   [Guide](https://github.com/flagos-ai/FlagScale/blob/main/examples/robobrain_x0/README.md#serving)| ❌ |
| Qwen-GROOT | VLA | [Huggingface](https://huggingface.co/Qwen/Qwen3-VL-4B-Instruct) | ✅︎  [Guide](https://github.com/flagos-ai/FlagScale/blob/main/examples/qwen_gr00t/README.md#training) | ✅ [Guide](https://github.com/flagos-ai/FlagScale/blob/main/examples/qwen_gr00t/README.md#inference) | ✅   [Guide](https://github.com/flagos-ai/FlagScale/blob/main/examples/qwen_gr00t/README.md#serving)|  ❌ |
| GR00T-N1.5 | VLA | [Huggingface](https://huggingface.co/nvidia/GR00T-N1.5-3B) | ✅︎  [Guide](https://github.com/flagos-ai/FlagScale/tree/main/examples/gr00t_n1_5#training) | ❌ | ✅   [Guide](https://github.com/flagos-ai/FlagScale/tree/main/examples/gr00t_n1_5#serving)|  ❌ |
