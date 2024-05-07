#How to build a dron?

#材料:
機載電腦(樹梅派)
飛控板:Pixhawk 2.4.8、4、mini 4
鋰電池
電調、遙控器(接收器)、配電板、降壓模組
WIFI卡

#Pixhawk2.4.8
![image](https://github.com/Pp7887139/my-ros-drone-note/assets/134500400/43b81afd-f5e9-4064-9bae-f09fbfe4624e)

#上圖概念說明:以四旋下無人機做說明

mainout接口:主要作為電機馬達的控制。1、2、3、4對應到電調，再對應到四個電機

RCIN接口:對應遙控機接收器

Buzzer接口:作為蜂鳴器接口，用來作為提示的聲音(例如開機、警報音、位置提示音等等

TELEM2接口:作為連接到機載電腦(樹梅派)的數據線。通常做為計算通信接口。

需要通過TTL進行轉換才可接到機載電腦上的USB接口(USB2)。

SERIAL4/5接口:連接到機載電腦端的USB3，作為擴展功能的接口

TELEM1接口:可做為WIFI接口OR一對一接口(上圖為一對一)

GPS接口:就是接GPS...

SWITCH按鈕:為安全開關，若是需要正常使用，需要切掉

POWER接口:作為充電供電口。

機載電腦供電:透過厘電池經過經過降壓模塊後，進行供電

深度鏡頭:經由USB1接到機載電腦上，就可在無GPS情況下為無人機提供位置數據

整體供電:透過鋰電池經由配電板，分送至各個配件

##Pixhawk4

![image](https://github.com/Pp7887139/my-ros-drone-note/assets/134500400/4fe8852a-6338-471b-9dcf-a6a350bd83b1)

#上圖概念說明:以四旋下無人機做說明

Power1接口:經由配電板分電後輸入的主電源。Power2不做使用

TELEM1接口:做為WIFI傳輸口，供電是利用分電板單獨供電

UART&I2CB接口:為供能擴展接口，可外接其他設備

TELEM2接口:連接到機載電腦

DSM/SUBS RC接口:衛星功能相關接口

PPM RC接口:對應遙控機接收器上PPM接口

GPS MOUDLE接口:就是接GPS..

IO PWM OUT接口:為電調信號的控制接口。

電調:電機接法為13、24對角線接法

板載計算機:傳感器接法基本與2.4.8一致
