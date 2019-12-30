## 1.参考论文
****
模型预测控制
虚拟模型控制
## 2.身体位姿规划
****
通过二次规划求解静步态身体质心位置。（OOQP）
动步态：虚拟支撑区域，通过设置权重（根据接触相和摆动相），将机器人四条腿设置成四个虚拟落脚点。
## 3.运动控制
****
（摆动腿-->落脚点）（支撑腿-->身体位姿调整)

<font color=#0000FF >3.1</font>通过PD控制和动力学前馈，完成机器人的单腿逆运动学（KDL求解运动学）（RBDL求解动力学）
<font color=#0000FF >3.2</font>通过规划器给出期望位姿和速率，通过PD控制和动力学前馈给出身体的控制率，然后通过运动平衡方程算出单腿的控制力（<font color=#FF0000 >不能获得唯一解析解</font>）。
<font color=#0000FF >3.3</font>二次规划的虚拟模型控制：寻找最优解。
## 4.控制系统
****
<font color=#0000FF >4.1</font>
用户交互层
<font color=#0000FF >4.2</font>
运动规划层
腿部关节、足端、身体位姿
<font color=#0000FF >4.3</font>
实时控制层
腿部关节、足端、身体位姿
<font color=#0000FF >4.4</font>
硬件驱动层
主站：NUC
从站：
收发同步，每次发送控制指令时读取反馈数据。