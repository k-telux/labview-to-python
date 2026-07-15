# LabVIEW 转 Python 工业软件 Skill

[English](../README.md) | 简体中文 | [日本語](README.ja-JP.md)

这是由 **telux** 创建的一套证据门禁式 Agent Skill 与工业软件规则，用于把
LabVIEW 实验室/工业测量程序迁移为 Python，同时保留测量逻辑、数据血缘、
硬件安全、UI 可用性和最终 EXE 的运行证据。

本页是社区翻译摘要；出现歧义时以英文 `SKILL.md` 为准。

## 核心原则

- 先迁移 VI/subVI 的真实行为和数据处理，再优化 UI。
- 工业 UI、LabVIEW 复刻 UI、模拟器和真实硬件共用同一 workflow。
- quick preview 只验证交互，不能证明完整分辨率或完整数据。
- 目标 CSV 回灌属于 roundtrip fixture，不能冒充独立 LabVIEW 算法等价。
- UI 必须用真实点击、输入、滚动、下拉和鼠标悬停，并进行截图人工二审。
- 源码 UI、模拟器、EXE、真实硬件和未验证子系统分别报告。

## 安装

```bash
npx skills add k-telux/labview-to-python-industrial-skill \
  --skill labview-to-python-industrial \
  --agent codex
```

也可以把 `skills/labview-to-python-industrial` 复制到 Codex 的 skills 目录，
并把 `rules/labview-to-python-industrial.zh-CN.md` 放进项目的长期规则入口。

## 使用示例

```text
使用 $labview-to-python-industrial 审核这个 LabVIEW 转 Python 项目。先证明
resolved scan plan、硬件调用顺序、数据与保存一致，再验证源码 UI 和 EXE；
没有真实硬件时保持 real_hardware_unvalidated_blocked。
```

真实项目脱敏示例见 [examples](../examples/README.md)，完整英文规范见
[SKILL.md](../skills/labview-to-python-industrial/SKILL.md)。
