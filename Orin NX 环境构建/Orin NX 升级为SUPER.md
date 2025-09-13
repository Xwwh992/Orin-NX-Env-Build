### 完成刷jetpack的前置操作

https://www.notion.so/SDK-manager-Jetpack-873047bff21d46aaa6885549d07cb76d?pvs=4

### 刷写

刷jetpack可以由TF卡刷写，SDK manager，脚本刷写。SDKmanager比较简单且流程完备，脚本刷写定制程度高。采用脚本刷写jetpack的方式才能升级到super。

在下面的页面下载

https://developer.nvidia.com/embedded/jetson-linux-r3643

![image-20250913195329005](/home/wyc/.config/Typora/typora-user-images/image-20250913195329005.png)

然后在下载下来的位置打开终端，依次输入如下命令

```bash
tar xf Jetson_Linux_R36.4.3_aarch64.tbz2

sudo tar xpf Tegra_Linux_Sample-Root-Filesystem_R36.4.3_aarch64.tbz2  -C  Linux_for_Tegra/rootfs/

cd  Linux_for_Tegra/

sudo ./tools/l4t_flash_prerequisites.sh

sudo ./apply_binaries.sh

sudo ./tools/kernel_flash/l4t_initrd_flash.sh --external-device nvme0n1p1 -c tools/kernel_flash/flash_l4t_t234_nvme.xml -p "-c bootloader/generic/cfg/flash_t234_qspi.xml"  --showlogs --network usb0 p3768-0000-p3767-0000-super internal
```

等待烧录完成之后键鼠操作设置linux基本设置，然后取下跳线帽关机然后正常开机

### 安装jetpack组件

```bash
sudo apt update

sudo apt install nvidia-jetpack
```

**额外说明**：

能否成功进入刷写可能和供给电压有关系，12v和19v电压都可以尝试，跳线帽要固定牢固，不然会出现无法进入RCM，需要下载Secure boot文件等情况



### 参考

https://blog.csdn.net/weixin_48208348/article/details/145275360

https://www.bilibili.com/video/av113968047723383/?vd_source=b5dd32c2e7c8002c88959ffed7c2af80