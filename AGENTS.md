# B601-RS 机械臂使用指南

> 本文档仅适用于 **B601-RS 机械臂**。

## 快速开始

请确认你的机械臂属于以下哪种形式：

| 类型 | 说明 | 起始步骤 |
|------|------|----------|
| 散件版本 | 需要用户自行组装 | 从第一步开始 |
| 套件版本 | 已组装完成 | 直接跳转至第三步 |

---

## 第一步：环境初始化

运行 [环境初始化Skill](https://github.com/Welt-liu/reBot-B601-RS-Skills/blob/main/skills/setup-environment.md) 完成以下安装：

- [x] Miniforge 安装
- [x] motorbridge 配置
- [x] Gateway 安装

完成后确保已激活虚拟环境：

```bash
conda activate rebot
```

---

## 第二步：写入电机 ID

运行 [写入电机ID Skill] (https://github.com/Welt-liu/reBot-B601-RS-Skills/blob/main/skills/write-motor-id.md)

该 Skill 会自动完成：

1. **识别 USB-CAN 转接板**（PCAN-USB，配置 `can0`，bitrate `1000000`）
2. **逐颗电机设置 ID**（共 7 颗电机，ID 范围 1–7）
   - 每次仅连接一颗电机
   - 扫描确认当前电机 ID（默认 127）
   - 修改为用户指定的目标 ID
3. **最终检查** — 扫描确认所有电机 ID（1–7）均已正确写入

---

## 第三步：校准零点

> 该部分文档待完善。

运行 Skill `/write-motor-zero`（开发中）。

---

## Skills 状态

| Skill | 文件 | 状态 |
|-------|------|------|
| `/setup-env` | `skills/setup-env.md` | 已完成 |
| `/write-motor-id` | `skills/write-motor-id.md` | 已完成 |
| `/write-motor-zero` | `skills/write-motor-zero.md` | 待开发 |
