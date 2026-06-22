# 🤖 少儿科创教育知识库 (Kids STEM Education Knowledge Base)

> 为 4-12 岁孩子打造的机器人与科创启蒙路径，基于"实践中学习"理念，实验驱动、先玩后懂、软硬结合。

[![Obsidian](https://img.shields.io/badge/Obsidian-知识库-purple)](https://obsidian.md/)
[![License: CC BY-NC-SA 4.0](https://img.shields.io/badge/License-CC%20BY--NC--SA%204.0-lightgrey.svg)](https://creativecommons.org/licenses/by-nc-sa/4.0/)

## 📖 知识库简介

本知识库为有技术背景的家长（尤其是软件工程师）提供了一套完整的少儿科创教育框架，涵盖：

- **白名单赛事**：教育部 2025-2028 学年竞赛活动名单中与机器人/AI/编程相关的赛事
- **核心概念**：创客教育、STEAM、建构主义、计算思维等教育理论
- **硬件百科**：19 种常用传感器与执行器，含儿童友好解释和技术参数
- **学习路径**：为 4 个不同年龄段孩子定制的渐进式学习路径
- **家长指南**：认知发展、安全指南、竞赛备赛、资源汇总

## 🗂️ 目录结构

```
maker-plan/
├── 000-Home-MOC.md                    # 总入口 (Map of Content)
│
├── 01-White-List-Competitions/        # 白名单赛事库 (10 项)
│   ├── 01-AI-Innovation-Challenge.md  # 全国青少年人工智能创新挑战赛
│   ├── 02-WRC-Robot-Design.md         # 世界机器人大会青少年机器人设计大赛
│   ├── ...
│   └── 10-AI-Digital-Art.md           # 全国青少年人工智能辅助生成数字艺术创作者大赛
│
├── 02-Concepts/                       # 核心概念库 (8 项)
│   ├── 创客教育.md                     # Maker Education
│   ├── STEAM教育.md                   # STEAM Education
│   ├── 建构主义.md                     # Constructionism
│   ├── 做中学.md                       # Learning by Doing
│   ├── 计算思维.md                     # Computational Thinking
│   ├── 机器人教育.md                   # Robotics Education
│   ├── 不插电编程.md                   # Unplugged Coding
│   └── 实体计算.md                     # Physical Computing
│
├── 03-Hardware-Sensors/               # 传感器与执行器百科 (19 项)
│   ├── 超声波传感器.md                 # HC-SR04 Ultrasonic
│   ├── 红外循迹传感器.md               # IR Line Tracking
│   ├── 舵机.md                        # Servo Motor
│   ├── ...
│   └── 继电器模块.md                   # Relay Module
│
├── 04-Learning-Paths/                 # 学习路径
│   ├── Track-A-4yo/                   # 4岁幼儿园路径 (6 节点)
│   │   ├── Track-A-Overview.md
│   │   ├── A01-认识方向.md
│   │   ├── ...
│   │   └── A06-玛塔编程启蒙.md
│   │
│   ├── Track-B-7yo/                   # 7岁小学二年级路径 (8 节点)
│   │   ├── Track-B-Overview.md
│   │   ├── B01-Hello-Micro-bit.md
│   │   ├── ...
│   │   └── B08-循迹小车入门.md
│   │
│   └── Track-C-8yo-MicroPython/       # 8岁 MicroPython 进阶路径 (10 节点)
│       ├── Track-C-Overview.md
│       ├── C01-MicroPython入门.md
│       ├── ...
│       └── C10-智能家居原型.md
│
└── Track-D-10yo-Advanced/             # 10-12岁竞赛冲刺路径 (10 节点)
    ├── Track-D-Overview.md
    ├── D01-Python进阶语法.md
    ├── ...
    └── D10-综合冲刺.md
│
└── 05-Parent-Guide/                   # 家长指南 (8 项)
    ├── 儿童认知发展指南.md
    ├── 电子安全指南.md
    ├── 竞赛备赛指南.md
    ├── 中国创客资源大全.md
    ├── 开源课程资源.md
    ├── 学习评估方法.md
    └── 屏幕时间与数字健康.md
```

## 🎯 四条学习路径

### Track A：4岁（幼儿园小班）
- **核心目标**：触觉感知、空间建构、逻辑启蒙
- **方向**：大颗粒机械结构、逻辑积木（玛塔创客、乐高 Coding Express）
- **特点**：不插电活动为主，屏幕时间极少

### Track B：7岁（小学二年级，零基础）
- **核心目标**：兴趣激发、传感器认知、初级图形化编程
- **方向**：Micro:bit 或乐高 Spike Essential
- **特点**：从单传感器互动过渡到简易小车

### Track C：8岁（有机器人基础，刚接触 MicroPython）
- **核心目标**：图形化向代码过渡、开源硬件探索、工程思维
- **方向**：MicroPython 进阶控制、自主循迹/避障小车、IoT 微型项目
- **特点**：软硬结合，逐步深入原理

### Track D：10-12岁（竞赛冲刺）
- **核心目标**：Python进阶、C++入门、竞赛备战、综合项目
- **方向**：复杂算法、AI应用、系统设计、工程笔记
- **特点**：竞赛驱动，冲刺白名单赛事国家级奖项

## 🔗 双向链接

本知识库充分利用 Obsidian 的双向链接功能：

- 赛事笔记 → 链接到推荐的硬件/路径
- 路径节点 → 链接到传感器百科
- 实验代码 → 链接到概念库
- 概念笔记 → 链接到相关赛事和路径

在 Obsidian 中打开本知识库，即可通过关系图谱查看所有笔记的关联关系。

## 🚀 快速开始

1. **安装 [Obsidian](https://obsidian.md/)**
2. **打开本文件夹作为 Vault**
3. **从 `000-Home-MOC.md` 开始浏览**
4. **根据孩子年龄选择对应的学习路径**

## 📚 数据来源

- 教育部官网 (moe.gov.cn) - 2025-2028 学年竞赛白名单
- 中国电子学会、中国计算机学会等官方资料
- Micro:bit Foundation、Arduino Education、Raspberry Pi Foundation
- IEEE、ACM 等学术期刊的教育研究论文
- AAP、WHO 等权威机构的儿童发展指南

## 🤝 贡献

欢迎提交 Issue 和 Pull Request！

如果你有：
- 新的赛事信息
- 更好的实验设计
- 错误修正
- 翻译改进

请直接提交 PR 或开 Issue 讨论。

## 📄 许可证

本作品采用 [知识共享署名-非商业性使用-相同方式共享 4.0 国际许可协议](https://creativecommons.org/licenses/by-nc-sa/4.0/) 进行许可。

您可以自由地：
- **共享** - 在任何媒介以任何形式复制、发行本作品
- **演绎** - 修改、转换或以本作品为基础进行创作

惟须遵守下列条件：
- **署名** - 您必须给出适当的署名
- **非商业性使用** - 您不得将本作品用于商业目的
- **相同方式共享** - 如果您修改本作品，必须以相同许可协议分发

## 🙏 致谢

感谢以下开源社区和教育资源：
- [Micro:bit Educational Foundation](https://microbit.org/)
- [Arduino Education](https://www.arduino.cc/education)
- [Raspberry Pi Foundation](https://www.raspberrypi.org/)
- [CS Unplugged](https://www.csunplugged.org/)
- [Code.org](https://code.org/)

---

**最后更新**：2026年6月22日

**维护者**：[@zernel](https://github.com/zernel)
