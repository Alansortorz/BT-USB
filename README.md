# BT-USB

一个用来蓝牙转USB串口的模块，用来进行无线数据传输，无线调参的装置，硬件已经测试通过~

## 效果图
硬件部分采用一个HC05模块，串口芯片用的CH340T。其实串口芯片用CP2102可能减少一些不必要的麻烦，虽然这个芯片的价格会贵一点。
最后的成品是这样的：
<div align=center><img src="https://user-images.githubusercontent.com/48275625/146016455-b6106ac0-f518-4c91-b779-fcc6a29c2d5c.jpg" width="200"></div>

背面实物图是这样的：
<div align=center><img src="https://user-images.githubusercontent.com/48275625/146016411-9f1a089f-d2ad-4909-a261-41eb10272a96.jpg" width="200"></div>

原本设计的3D渲染图是这样的：
<div align=center><img src="https://user-images.githubusercontent.com/48275625/146016543-b56d4d8d-dc6b-4163-aba2-79425c398ec5.jpg" width="200"></div>

背面的3D渲染图：
<div align=center><img src="https://user-images.githubusercontent.com/48275625/146016560-02f262bb-afa4-4cd4-adea-648058302069.jpg" width="200"></div>


## 注意点
已经测试通过了，正常可用，下面有几点补充：


（1）蓝牙模块的RX接CH340T的TX，蓝牙模块的TX接CH340T的RX

（2）蓝牙的基本操作

大家都知道蓝牙分通讯模式和AT指令模式，按住BT-USB的按键，插入电脑，红色指示灯一秒翻转一次表明进入AT模式，通过以下操作配置蓝牙模块

1 AT+ORGL             恢复出厂设置

2 AT+ROLE=1           设置模块为主模式

3 AT+PSWD="0000"      连接密码，这里自己设置，需要和从机地址一致

4 AT+UART=38400,0,0   设置通讯波特率，停止位和校验位

5 AT+BIND=2020,8,24585绑定从机地址

6 AT+CMODE=0          表明蓝牙模块通过物理地址来进行连接


从机就是即的机器人或者小车那部分的蓝牙模块，配置就比较简单

1 AT+ORAL

2 AT+ROLE=0         设置为从机

3 AT+PSWD="0000"    配置连接密码

4 AT+UART=38400,0,0 配置串口

5 AT+ADDR?          这一步是查看从机的地址，在主机的第五步进行配置

6 AT+CMODE=1        任意蓝牙地址连接，因为它是被连接，而不是去连接别人

整个小项目并不复杂，只有硬件，没有软件，作为一个辅助工具还是非常的Nice的~。值得注意的是CH340T芯片需要配备12MHz的晶振，其他频率的都不可以，如果你的电脑显示不能识别的设备，可能就是这个晶振的缘故了
