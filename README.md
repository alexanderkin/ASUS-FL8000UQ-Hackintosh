# macOS Mojave/Catalina/Big Sur For ASUS-FL8000UQ-Hackintosh

# BIOS设置：

- 关闭`SecureBoot`

- 关闭`FastBoot`

- 解锁`CFG Lock`

  1.将U盘格式化为FAT32格式；

  2.打开CFG文件夹，将里面的EFI文件复制到U盘中，重启按ESC键选择U盘启动；

  3.输入命令`setup_var_3 0x527 0x00`即可解锁CFG Lock。

## 一、配置：

|    配置       |        型号                 |
|--------------|-----------------------------|
|    处理器     |          i7-8550U           |
|     核显      |    Intel Graphics UHD620    |
|     独显      |    GeForce 940MX（已屏蔽）    |
|     内存      |     4G×2 DDR4 2400MHz       |
|     硬盘      |       120G SSD/1T HDD       |
|     声卡      |       Realtek ALC294        |
|   无线网卡     |        BCM943602CS      |

关于拆机卡BCM943602CS和BCM943602CDP导致在关机状态下拔插电源适配器电脑自动开机的情况，第一种方法是屏蔽拆机卡的第13针脚，屏蔽后即可解决此问题，第二种方法是屏蔽转接卡的第54针和第55针，同样可以解决此问题。推荐使用DW1820A-08PKF4版本，无需屏蔽针脚，稳定运行。

![2.png](https://github.com/KKKIIINNN/ASUS-FL8000UQ-Hackintosh/blob/master/screenshot/2.png)

## 二、正常工作
1. CPU变频
2. 核显硬件加速，独显无法驱动已做屏蔽
3. 声卡输出（~~自编译AppleALC驱动~~  已合并至[`AppleALC`](https://github.com/acidanthera/AppleALC)，LayoutID=66）
4. HDMI输出
5. USB
6. WIFI/蓝牙(已更换BCM943602CS,原装AR9565可驱动,有需要可去远景论坛查找）
7. 电量显示正常
8. 触控板
9. 睡眠和唤醒
## 三、一键开启HIDPI项目地址：[`one-key-hidpi`](https://github.com/xzhih/one-key-hidpi)
macOS Big Sur请使用[`原版镜像生成ISO文件和一键开启HIDPI`](http://bbs.pcbeta.com/forum.php?mod=viewthread&tid=1862620&highlight=HIDPI)来开启HIDPI
## 四、关于F5~F12的问题。
已添加SSDT加载苹果F5~F12按键功能，不再使用Fn组合键。  
|    按键   |        功能            |
|----------|------------------------|
|   F5     |    Brightness_down     |
|   F6     |    Brightness_up       |
|   F7     |    Scan Previous Track |
|   F8     |    Play/Pause          |
|   F9     |    Scan Next Track     |
|   F10    |    Mute                |
|   F11    |    Volume_down         |
|   F12    |    Volume_up           |


如果需要用到这些按键原本的功能的话，可以删除ACPI文件下的SSDT-Fkey.aml,然后使用Karabiner Elements来进行键位调整，这样就能在使用原本功能的同时也支持Mac的功能。
## 五、注意事项
1.下载的EFI请替换其中的三码后再使用，防止出现冲突。  
2.BIOS309无法安装的问题已经修复，不需要再在win10里面禁用“更新不包括驱动程序”了。  
3.安装完成后请使用Hackintool重新定制USB以解决睡眠问题：[`USB定制教程`](https://blog.daliansky.net/Intel-FB-Patcher-USB-Custom-Video.html)   
4.OpenCore关闭"Msic->ShowPicker"后可在开机过程中在ASUS标志出来后用alt键来显示启动菜单，笔记本自带键盘需要长按alt键，外接键盘需要不断点按alt键。  
5.Windows+Mac双系统推荐使用NDK-OpenCore，对windows没有影响。原版OpenCore可能导致windows激活信息丢失。  
6.macOS Big Sur在安装过程中如果出现内核崩溃情况只需要清理一次NVRAM即可。  
7.由于现在的OC重命名较多，请尽量不要使用OC引导Windows，否则可能会出现意外情况。  
8.DW1820A需要先屏蔽针脚，因为EFI文件中如果没有驱动的话会导致进系统禁行，卡顿等，进入系统驱动完成后就可以不用屏蔽针脚了。

## 六、HDMI注意事项
此电脑在BIOS中打开CSM兼容选项就可以在外接显示器中显示BIOS和Clover界面以及开机过程，但如果用外接显示器开机，那么黑苹果内屏将无法使用，但是10.14 Mojave中在clover里加上“igfxcflbklt=1”启动参数，开机后将笔记本盖子合上再打开即可同时使用内外屏，但注意，加上此启动参数后亮度调节将失效。此方法在10.15 Catalina中无效，所以建议10.15 Catalina不要打开CSM兼容模式，用内屏来开机，等黑苹果完全启动即可使用外屏。
## ~~七、关于睡眠过程中自动唤醒解决方案~~(貌似没啥用)
当电脑出现自动唤醒后，打开终端输入 log show --last 1d | grep "Wake reason" 找到唤醒电脑的设备，然后在DSDT中搜索对应的设备，将设备下面的_PRW方法注释掉即可。
## 八、本机NVRAM在Mac下可以正常使用，可以可在偏好设置中使用“启动磁盘”来设置默认启动项。
## 九、截图
![1.png](https://github.com/KKKIIINNN/ASUS-FL8000UQ-Hackintosh/blob/master/screenshot/1.png)  
