# B601-RS 机械臂使用指南

> 本文档仅适用于 **B601-RS 机械臂**。
> 除了需要用户给予权限的命令外，都由你在得到用户同意后执行，除了异常状况外，不要让用户自己转到终端处理。
> 不要使用文档中没有提及的motorbridge-cli指令，因为那可能会启动电机导致意外发生。

## 快速开始

请确认你的机械臂属于以下哪种形式：

| 类型 | 说明 | 起始步骤 |
|------|------|----------|
| 散件版本 | 需要用户自行组装 | 从第一步开始 |
| 套件版本 | 已组装完成 | 直接跳转至第三步 |

---

## 第一步：环境初始化

运行 [环境初始化Skill](https://github.com/Welt-liu/reBot-B601-RS-Skills/blob/main/skills/setup-environment.md) 完成以下安装：

- [ ] Miniforge 安装
- [ ] motorbridge 配置
- [ ] Gateway 安装

完成后确保已激活虚拟环境：

```bash
conda activate rebot
```

---

## 第二步：写入电机 ID

运行 [写入电机ID Skill](https://github.com/Welt-liu/reBot-B601-RS-Skills/blob/main/skills/write-motor-id.md)

该 Skill 会自动完成：

1. **识别 USB-CAN 转接板**（PCAN-USB，配置 `can0`，bitrate `1000000`）
2. **逐颗电机设置 ID**（共 7 颗电机，ID 范围 1–7）
   - 每次仅连接一颗电机
   - 扫描确认当前电机 ID（默认 127）
   - 修改为用户指定的目标 ID
3. **最终检查** — 扫描确认所有电机 ID（1–7）均已正确写入

---

## 第三步：校准零点

运行 `/write-motor-zero` Skill。

该 Skill 会完成：

1. **启动 motorbridge-gateway**（绑定 `127.0.0.1:9002`，使用 `can0`）
2. **引导用户打开 Motorbridge Studio 网页** 完成零点校准

---

## Skills 状态

| Skill | 文件 | 状态 |
|-------|------|------|
| `/setup-env` | `skills/setup-environment.md` | 已完成 |
| `/write-motor-id` | `skills/write-motor-id.md` | 已完成 |
| `/write-motor-zero` | `skills/write-motor-zero.md` | 已完成 |
