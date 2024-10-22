# 键盘按键延迟测试工具

## 硬件配置
* 雅特力 AT-START-F405 V1.0 开发板（1套）；
* 光电隔离触发按键模组（1个）；
* 串口线（至少需可以连接到开发板的TX串口）（1条）；
* USB type-C 线 （1条）；
* 待测试键盘（若干）；

## 搭建硬件平台
* 连接串口线的RX到开发板上标示为“AT-Link”插孔的TX信号孔上，连接双方GND到一起；
* 连接串口线到监视电脑上，监视串口数据；
* 连接光电隔离触发按键模组的红线端子到开发板上J2 排针的B13脚上，连接黑线端子到J2排针的GND引脚上；
* 待测试键盘的 typeA 型USB插头插到开发板上标示为HS_HOST的USB Type A插座上；

* 安装仿真按键到待测键盘上：
* * 拔掉待测试键盘上主键区（26个字母和数字整合的区域）的任意一颗字母或数字按键（可能需要借助拔键器先拔掉键帽，再借助拔轴器把按键开关拔下来）；
* * 把光电隔离触发按键模组的仿真开关插入到键盘上拔掉按键的位置，注意插入的方向避免开关的引脚不能插入到板上的轴脚孔内；

* 硬件环境搭建如下图：
![按键延迟测试](https://i.imgur.com/NiOZuJj.jpeg)

## 固件开发环境
* 本项目是基于雅特力 Plateform-arteryat32 环境开发的，具体环境安装请参考官方的 [环境安装说明](../../README.md)；
* 需确保已经正确安装了PlateformIO的扩展，如未安装，可以在VS code 扩展应用中搜索PlateformIO IDE,并按照提示进行安装；

## 测试说明
* 正确烧录该项目固件到开发板上后，按下开发板上的RESET（B1）按钮，可以在监视器上看到键盘设备的相关信息：
  * This is a xxxx device
  * USB Device Attached
  * VID: xxxx
  * PID：xxxx
  * Set Address: xxxx
  * Manufacturer: xxxxx
  * Product: xxxx
  * Serial: xxxx
  * Enumeration done
  * Keyboard Device
* 当监视器上能正常显示这些信息，说明键盘连接正常，按下USER（B2）按钮，监视器上会显示如下信息：
  * Start testing key delay time
  * Capture key is [x]
  * The Key received delay time is [xxxx] uS
* 这个信息就显示了当前测试的是“X”键，这个键从用户按下开始到测试工具识别到它共花费了xxxxuS的时间，这个时间就我们所要测试的延迟时间。
-----------------------------------------------------
 #### 注意：由于键盘和主机的通讯是查询的方式，以及测试工具处理数据需要占用一定的时间，所以所测试到的延迟时间可能会有约1-2个数据帧的误差。
