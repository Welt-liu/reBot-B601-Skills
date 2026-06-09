# 零点校准

conda activate rebot
这一步使用如下命令


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


```bash
conda activate rebot
motorbridge-gateway -- --bind 127.0.0.1:9002 --transport socketcan --channel can0  
```

然后提示用户打开网页 https://motorbridge.github.io/motorbridge-studio/