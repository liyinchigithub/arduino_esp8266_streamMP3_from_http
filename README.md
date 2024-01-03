# 基于ESP8266 开发板（MCU）实现音频流在线播放

* 8266 wifi 主板

<img src="https://github.com/liyinchigithub/arduino_8266_wifi_http/assets/19643260/76239ce4-ee90-4eb4-8592-a552edf20d79" width="500" height="500">

## 引脚图

<img src="https://github.com/liyinchigithub/arduino_8266_wifi_http/assets/19643260/bb6bba64-6fff-4bb0-8efd-cd1b91b4743d" width="500" height="500">

## 安装ESP8266Audio库

1. 打开Arduino IDE。

3. 在菜单栏中，选择Sketch -> Include Library -> Manage Libraries...。

5. 在弹出的库管理器窗口中，输入ESP8266Audio库到搜索框中。

7. 在搜索结果中找到ESP8266Audio by Earle FPhlhower，点击Install按钮进行安装。


## 选择开发板

1. 打开Arduino IDE。

2. 在菜单栏中，选择工具 -> 开发板 -> 选择NodeMcu1.0

![image](https://github.com/liyinchigithub/arduino_8266_wifi_http/assets/19643260/28203800-5c51-43a8-8af3-ba9499a6872a)

## （三）选择端口

![image](https://github.com/liyinchigithub/arduino_8266_wifi_http/assets/19643260/a6f60b7d-fe45-4a72-bc83-d17902110132)

# 麦克风

喇叭，有三个引脚最左边是GND、中间是VCC、最右边是SIG

按照以下方式将喇叭连接到ESP8266：

1. 将喇叭的GND（地线）连接到ESP8266的GND。
2. 将喇叭的VCC（电源）连接到ESP8266的3V3（3.3伏特电源）。
3. 将喇叭的SIG（信号）连接到ESP8266的RX（接收）

在代码中，正在使用AudioOutputI2SNoDAC类来处理音频输出。这个类默认使用ESP8266的I2S接口，该接口的数据引脚是GPIO3（即RX）。

所以，你的代码已经默认使用RX引脚作为音频输出。

你不需要做任何修改，只需要将你的喇叭的SIG引脚连接到ESP8266的RX引脚即可。

如果你想明确指定使用RX引脚，你可以在创建AudioOutputI2SNoDAC对象时传入参数，如下：

```C++
out = new AudioOutputI2SNoDAC(0, 1); // 第一个参数是左声道引脚，第二个参数是右声道引脚。0表示不使用，1表示使用RX引脚。
```


# 常见问题


在Arduino代码上传过程中，如果你的喇叭发出沙沙声，这可能是由于以下原因：

1. 串口通信干扰：在上传代码时，ESP8266的RX引脚会被用于串口通信。如果你的喇叭连接到了RX引脚，串口通信的电信号可能会被喇叭解释为音频信号，从而产生沙沙声。

2. 电源不稳定：上传代码时，ESP8266可能会消耗更多的电力，如果电源供应不稳定，可能会导致喇叭发出沙沙声。

为了避免这个问题，你可以在上传代码时断开喇叭和ESP8266的连接，等代码上传完成后再连接喇叭。或者，你可以尝试使用一个稳定的电源供应。
