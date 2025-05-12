#環境搭建

本次實驗採Anaconda+pychm做為開境
並使用gpu作為圖形辨識運算

#開發軟體下載:

Anaconda https://www.anaconda.com/ 

Pycharm https://www.jetbrains.com/pycharm/\


#檢查cuda版本(有兩種方法)

(1)在桌面右鍵點擊NVIDIA控制面板

![image](https://github.com/Pp7887139/my-ros-drone-note/assets/134500400/e6c4748d-a0a5-4903-8ea2-fafa3bc84101)

點擊系統資訊進入後按下元素

![image](https://github.com/Pp7887139/my-ros-drone-note/assets/134500400/5da77aae-82fd-49b8-8e32-58ee3c4a739a)

就可以查看到自己的cuda版本

(2)進入CMD，並輸入nvidia-smi
![image](https://github.com/Pp7887139/my-ros-drone-note/assets/134500400/c78eeb50-0c9d-4324-8571-702383e277d2)

也可以查看到自己的cuda版本


#下載cuda

https://developer.nvidia.com/cuda-toolkit-archive

在官網找到自己對應的版本下載並安裝

注意:安裝時要特別注意下載的路徑(之後設定環境變數時會用到)可以先拍照下來

#檢查cuda環境

在搜尋輸入編輯系統環境變數，就可以看到剛才安裝的cuda(若是沒有看到則需要手動添加)

![image](https://github.com/Pp7887139/my-ros-drone-note/assets/134500400/4e2aaa56-5660-448c-ba4b-c7d467576d0e)

進入CMD後輸入 nvcc --verison或者nvcc -V 檢查安裝的cuda版本

![image](https://github.com/Pp7887139/my-ros-drone-note/assets/134500400/806fdd40-c7ff-48c5-b9e4-c931addd4f23)

#CUDnn下载

https://developer.nvidia.com/cudnn-downloads

![image](https://github.com/Pp7887139/my-ros-drone-note/assets/134500400/97493673-eb1b-47f2-b0fe-16902d5196f5)

#檢查CUDnn環境

進入CMD輸入CD ...進到安裝目錄下、或是在安裝目錄下直接以CMD開啟

![image](https://github.com/Pp7887139/my-ros-drone-note/assets/134500400/652b5d08-10f6-4391-9b34-d5ebd16c0eb4)

之後再安裝目錄下執行:bandwidthTest.exe和deviceQuery.exe

![image](https://github.com/Pp7887139/my-ros-drone-note/assets/134500400/f394e8e8-9c64-4c1f-bc9f-7a5c73826dbf)

![image](https://github.com/Pp7887139/my-ros-drone-note/assets/134500400/610953e5-1935-43b8-945f-30842c8fd17d)

分別執行後，在result看見pass就代表安裝成功了!

到此yolov7的深度學習環境配置就完成了~







