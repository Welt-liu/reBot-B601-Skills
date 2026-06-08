# 写入电机 ID

## 使用前提

已执行 `/setup-env` Skill，完成环境安装。系统中应有 `rebot` 虚拟环境，开始前需执行：

```bash
conda activate rebot
```

## 目标设备：USB-CAN 转接板

通过以下特征识别目标设备：

```bash
# 套件里是 PCAN-USB，通常应直接出现 can0 或 can1
sudo modprobe peak_usb
ip -br link

# 如果出现 can0，设置 bitrate
sudo ip link set can0 down 2>/dev/null
sudo ip link set can0 type can bitrate 1000000 restart-ms 100
sudo ip link set can0 up

# 确认状态
ip -br link show can0
```

## 检查

执行以下命令：

```bash
motorbridge-cli scan --vendor robstride --channel can0 --start-id 1 --end-id 8
```
如果hit中1～7号电机，提示用户可能当前机械臂为成品版本，不需要修改id，本skill无需执行

## 修改电机 ID

机械臂共有 7 颗电机，需循环设置 ID，总共 7 次。用户分配的 ID 应为 1～7，每颗电机设置一个。

如果用户确认已有部分电机 ID 修改完成，可跳过已修改的电机。当 1～7 全部设置完成后，跳转至**检查**步骤。

### 连接新电机

1. 要求用户断电后拔掉当前电机上的线
2. 将线连接到下一颗电机
3. 等待用户接上电源后，执行**查找当前电机 ID**

### 查找当前电机 ID

执行前要求用户**只能连接一颗电机**。

```bash
motorbridge-cli scan --vendor robstride --channel can0 --start-id 126 --end-id 127
```

- **命中 127**：说明电机未设置过 ID，进入**修改当前电机 ID**步骤
- **未命中 127**：扫描 1～10，若命中其中某个 ID，说明用户已设置过该电机。提示用户命中的 ID，询问是否需要重新修改
- **命中多个电机**：异常状态，说明同时连接了多个电机，要求用户在断电后拔掉多余电机。

### 修改当前电机 ID

确认命中 127 后，要求用户给出新的 motor ID，填入 CLI 参数中：

```bash
# 示例：将 ID 127 改为 5
motorbridge-cli id-set --vendor robstride --motor-id 127 --new-motor-id 5
```

## 最后确认

执行以下命令：

```bash
motorbridge-cli scan --vendor robstride --channel can0 --start-id 1 --end-id 8
```

告知用户命中了哪些电机。用户确认无误后，本 Skill 执行完成；否则返回重新修改。
