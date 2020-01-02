#### 1框架
laikago的仿真节点图如图所示：   
![](assets/markdown-img-paste-20200101104606889.png)   
在节点图中，主要的数据流为  external_force -->gazebo<font color=#FF0000 ><--></font>servo   
从键盘上读取力，将力发布到/apply_force/trunk话题。  

servo从gazebo上订阅12个关节的状态、4个足端的力、IMU的状态。  
<font color=#FF0000 >在servo中，有一个未被发出的msg</font>。同时，发步了关节指令。

body.cpp定义了初始化函数（其中将关节状态赋值给关节命令）。
****
joint_controller:   
    首先，在init中从urdf中读取关节。然后将joint设置为hardware_interface的句柄，使joint可以调用hardware_interface的资源。并且订阅command命令，将订阅的msg通过回调函数赋值给lastCmd。   
    在starting中，读取硬件位置，并赋值给init_pos。同时将该位置赋值给lastCmd、lastState.
    在update中，用command读取实时指令并赋值给lastCmd。将lastCmd中的速度、位置、力矩赋值给servoCmd。   
    通过joint读取硬件当前的位置赋值给currentPos，通过currentPos、lastState.pose、lastState.velocity, period计算当前速度。通过当前位置、速度和电机指令计算所需力矩，通过joint发布该力矩给硬件借口
