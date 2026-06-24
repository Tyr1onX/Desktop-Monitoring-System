# Desktop-Monitoring-System

**Status: Pre-research / System design project**

**当前状态：方案设计与预研阶段，暂未形成完整可运行系统。**

Desktop-Monitoring-System is a pre-research and system design repository for a desktop posture monitoring concept based on ESP32, Wi-Fi CSI signals, MQTT communication, a Python backend, data visualization, and a planned CNN-LSTM recognition model.

This repository is used to organize project ideas, architecture notes, module boundaries, and future implementation plans. It should not be treated as a completed or production-ready system.

## 项目简介

本项目设想通过 ESP32 采集 Wi-Fi Channel State Information (CSI) 信号，使用 MQTT 将采集数据传输到 Python 后端，再进行数据预处理、可视化展示和后续姿态识别模型研究。

当前仓库主要用于记录方案设计、技术预研和后续开发路线。现阶段暂未包含完整的固件、后端、模型训练和前端可视化实现。

## 背景与动机

久坐和不良坐姿可能影响学习、办公和身体健康。传统坐姿检测方式通常依赖摄像头、穿戴设备或压力传感器，可能存在隐私、佩戴体验或部署成本问题。

本项目预研 Wi-Fi CSI 在非接触式桌面坐姿监测场景中的可行性，探索是否可以通过无线信号变化感知人体姿态变化，并结合轻量级边缘硬件与后端分析流程形成一个实验性系统设计。

## 技术关键词

- ESP32 / ESP32-S3
- Wi-Fi CSI
- MQTT
- Python backend
- Paho-MQTT
- Matplotlib visualization
- Signal preprocessing
- Butterworth filter
- CNN-LSTM
- Posture recognition
- System design

## 系统架构

计划系统由以下部分组成：

```txt
ESP32 / ESP32-S3
  -> collect Wi-Fi CSI signal data
  -> package signal frames
  -> publish data through MQTT

MQTT broker
  -> receive CSI messages
  -> forward messages to subscribers

Python backend
  -> subscribe to MQTT topic
  -> parse CSI data
  -> preprocess and store samples
  -> provide data for visualization and model experiments

Visualization module
  -> display signal curves
  -> support manual observation during experiments

CNN-LSTM model research
  -> learn spatial and temporal patterns from CSI data
  -> explore posture classification feasibility
```

More architecture notes are available in [docs/architecture.md](docs/architecture.md).

## 模块设计

### ESP32 数据采集模块

设计为运行在 ESP32 / ESP32-S3 上，负责开启 Wi-Fi CSI 采集能力，读取原始 CSI 数据，并将数据整理成适合传输的消息格式。

### MQTT 通信模块

计划采用 MQTT 作为轻量级通信协议，用于连接硬件采集端和上位机 / 后端程序。预研方向包括 topic 设计、QoS 选择、消息格式和异常处理。

### Python 后端模块

设计为订阅 MQTT 数据流，完成数据解析、基础校验、缓存、记录和预处理。后续可扩展为数据集构建、实验管理和模型推理入口。

### 可视化模块

计划使用 Python 可视化工具展示 CSI 子载波幅值变化，帮助观察不同坐姿、距离和环境变化下的信号差异。

### CNN-LSTM 识别模块

计划用于预研基于 CSI 时序数据的姿态分类。CNN 可用于提取局部特征，LSTM 可用于建模时间序列变化。当前仅作为方案设计方向，尚未在仓库中形成完整训练或推理代码。

## 当前进展

- 已整理非接触式桌面坐姿监测的项目方向。
- 已预研 ESP32 Wi-Fi CSI、MQTT 通信、Python 可视化和 CNN-LSTM 姿态识别的技术路线。
- 已形成初步系统架构和模块划分。
- 当前仓库尚未包含完整可运行系统源码。
- 当前没有公开验证的准确率、稳定性或部署结果。

## 后续计划

- 补充 ESP32 CSI 采集固件原型。
- 设计 MQTT topic、消息格式和数据采样规范。
- 实现 Python 数据接收、保存和可视化脚本。
- 建立实验数据采集流程和标注规范。
- 预研 CSI 数据预处理方法，例如滤波、归一化和窗口切片。
- 尝试 CNN-LSTM 姿态识别实验，并记录实验条件和结果。
- 在具备完整代码和验证结果后，再补充运行说明与实验报告。

More details are available in [docs/roadmap.md](docs/roadmap.md).

## 项目限制

- 当前处于方案设计与预研阶段，不是完整产品。
- 当前仓库没有形成完整可运行系统。
- 当前未公开硬件实测数据集。
- 当前未提供经验证的识别准确率。
- 当前未声明系统已完成部署或稳定运行。
- CSI 信号容易受到环境、设备位置、人体距离和无线干扰影响，后续需要通过实验验证可行性。

## 文档

- [docs/proposal.md](docs/proposal.md): 项目方案书内容摘要
- [docs/architecture.md](docs/architecture.md): 系统架构设计
- [docs/roadmap.md](docs/roadmap.md): 后续计划
