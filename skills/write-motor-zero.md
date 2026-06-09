# 零点校准

## 使用前提

- 已完成 `/write-motor-id`，电机 ID 已正确写入
- `can0` 已配置且处于 UP 状态（第二步中已配置）

## 步骤

### 1. 激活环境并启动 Gateway

```bash
conda activate rebot
motorbridge-gateway -- --bind 127.0.0.1:9002 --transport socketcan --channel can0
```

Gateway 启动后保持运行，不要关闭该终端。

### 2. 打开 Motorbridge Studio

提示用户访问：https://motorbridge.github.io/motorbridge-studio/

通过网页界面完成零点校准操作。
