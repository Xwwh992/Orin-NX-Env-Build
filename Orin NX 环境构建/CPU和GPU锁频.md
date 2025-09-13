新建脚本

```
sudo nano /usr/local/bin/lock_freq.sh
```

粘贴以下内容：

```
#!/bin/bash

# CPU 锁频设置
CPU_FREQ=1984000
for cpu in /sys/devices/system/cpu/cpu[0-9]*; do
    echo userspace > $cpu/cpufreq/scaling_governor
    echo $CPU_FREQ > $cpu/cpufreq/scaling_min_freq
    echo $CPU_FREQ > $cpu/cpufreq/scaling_max_freq
done

# GPU 锁频设置
GPU_PATH="/sys/devices/platform/bus@0/17000000.gpu/devfreq/17000000.gpu"
GPU_FREQ=1173000000

echo userspace > $GPU_PATH/governor
echo $GPU_FREQ > $GPU_PATH/min_freq
echo $GPU_FREQ > $GPU_PATH/max_freq

```

保存退出后赋予执行权限

```
sudo chmod +x /usr/local/bin/lock_freq.sh
```

新建服务文件

```
sudo nano /etc/systemd/system/lock-freq.service
```

粘贴以下内容：

```
[Unit]
Description=Lock CPU and GPU Frequency
After=multi-user.target
Requires=nvargus-daemon.service

[Service]
Type=oneshot
ExecStart=/usr/local/bin/lock_freq.sh
RemainAfterExit=true

[Install]
WantedBy=multi-user.target

```

重新加载 systemd：

```
sudo systemctl daemon-reexec
sudo systemctl daemon-reload
```

启动服务（立即执行锁频）：

```
sudo systemctl start lock-freq.service
```

设置为开机启动：

```
sudo systemctl enable lock-freq.service
```



下面是查看各种信息的命令

```
1.找到GPU频率控制路径

find /sys -name "*gpu*" -type d

2.查看当前控制策略

cat /sys/devices/platform/bus@0/17000000.gpu/devfreq/17000000.gpu/governor

3.查看可支持的控制策略

cat /sys/devices/platform/bus@0/17000000.gpu/devfreq/17000000.gpu/available_governors

4.查看当前GPU频率

cat /sys/devices/platform/bus@0/17000000.gpu/devfreq/17000000.gpu/cur_freq

5.查看支持的GPU频率

cat /sys/devices/platform/bus@0/17000000.gpu/devfreq/17000000.gpu/available_frequencies

6.切换策略为用户手动

echo userspace | sudo tee /sys/devices/platform/bus@0/17000000.gpu/devfreq/17000000.gpu/governor

7.设置最大频率

echo <最大频率值> | sudo tee /sys/devices/platform/bus@0/17000000.gpu/devfreq/17000000.gpu/max_freq
echo <最大频率值> | sudo tee /sys/devices/platform/bus@0/17000000.gpu/devfreq/17000000.gpu/min_freq

8.设定开机设置最大频率

查看所有CPU的可用频率

cat /sys/devices/system/cpu/cpu0/cpufreq/scaling_available_frequencies
```

参考：

https://blog.csdn.net/qq_44998513/article/details/133842103