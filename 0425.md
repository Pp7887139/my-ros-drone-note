#無人機原理

![image](https://github.com/Pp7887139/my-ros-drone-note/assets/134500400/bf837bad-5719-450e-a66c-15f44cac3f7c)

上位机里面有一个完整的算法，如自主避障算法

飞控里面有正常的飞控程序

飞控和上位机之间通过数据线连接，具备数据传输的基础

飞控进行一些设置（这个后面会讲），使得飞控可以接受上位机控制

上位机运行特殊的程序，可以给无人机发送信号

上位机运行程序（包括通信程序和自主避障程序），控制无人机飞行

#撰寫PX4並在GAZEBO虛擬環境下執行
https://blog.csdn.net/weixin_55944949/article/details/132570487?ops_request_misc=&request_id=&biz_id=102&utm_term=px4&utm_medium=distribute.pc_search_result.none-task-blog-2~all~sobaiduweb~default-2-132570487.nonecase&spm=1018.2226.3001.4187
起飛旋停、以及降落

今天的問題:
make[2]: *** No rule to make target 'off_node/CMakeFiles/offb_node.dir/build'.  Stop.
CMakeFiles/Makefile2:1430: recipe for target 'off_node/CMakeFiles/offb_node.dir/all' failed
make[1]: *** [off_node/CMakeFiles/offb_node.dir/all] Error 2
Makefile:140: recipe for target 'all' failed
make: *** [all] Error 2
Invoking "make -j6 -l6" failed

Solve:
![image](https://github.com/Pp7887139/my-ros-drone-note/assets/134500400/ab12c40a-0ff7-48ae-af88-8e1ba2699dfc)

CMakeLists.txt文件寫法錯誤，將CATKIN_DEPENDS roscpp rospy tf turtlesim這行的註解打開，就可以正常編譯

今天的問題:
運行示範程式碼之後發現
RLException: [xx.launch] is neither a launch file in package [x] nor is [x] a launch file name

Solve:
進入本機.bashrc，檢查是否有無以下兩行，沒有的話就加進去
source ~/catkin_ws/devel/setup.bash
export ROS_PACKAGE_PATH=${ROS_PACKAGE_PATH}:~/catkin_ws/
重啟 .bashrc
