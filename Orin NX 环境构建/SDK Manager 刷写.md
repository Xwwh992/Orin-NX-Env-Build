在Ubuntu大于等于20.04的电脑上下载SDK manager deb安装

安装的时候一般需要装一个gtk

### 进入RC模式

利用杜邦线或者跳线帽将第三个和第四个口连接起来  FC_REC 和  GND

![image-20250913201502101](./images/image-20250913201502101.png)

然后把NX的c口用USB-C与Ubuntu电脑连接起来

### 使用SDK Manager

不选Host

![image-20250913201514659](./images/image-20250913201514659.png)

勾选需要下载的组件

![image-20250913201526067](./images/image-20250913201526067.png)

![image-20250913201533687](./images/image-20250913201533687.png)

给NX连接键鼠和显示器，选择Runtime的话，可以在显示器上配置用户名和密码

![image-20250913201545064](./images/image-20250913201545064.png)

把Ubuntu电脑和NX连接到同一网络 并在NX上查看IP填入到这里 用户名和密码填入上一步在显示器上配置的用户名和密码

![image-20250913201557518](./images/image-20250913201557518.png)

![image-20250913201603715](./images/image-20250913201603715.png)

![image-20250913201609171](./images/image-20250913201609171.png)

### 失败情况

![image-20250913201620708](./images/image-20250913201620708.png)

一般因为连接线不行，可以换一下，最好要USB-C线

### 参考

https://blog.csdn.net/qq_41263444/article/details/138301510