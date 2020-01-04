####作者所用理论/模型
  基于投影的分层任务空间逆动力学框架
  prioritized least square optimization
  并行任务执行（移动足端、保持姿态、优化关节力矩...）
  静态优化：能量效率、抗滑稳定性、
  高柔性串联弹性驱动器
  Precise torque and position controllability
####背景
#####1.1本体：
  目前的液压驱动，具有高输出刚度特性。这些执行机构固有安全特性非常差。
  SEA（串联柔性驱动）适合与环境和人类的交互，但是在控制方面，固有柔性对精确控制不利。控制系统带宽显著降低（由于机械低通滤波）。
#####1.2控制：
* 传统的位置控制不能适应环境，而力矩控制不仅可以适应环境，而且可以通过合理分配关节力矩和足端力矩来提高动态稳定性。
######1.2.1运动生成
* deals with general concepts to create the behavior of the system，no final realization.
  数值优化。
  实时控制的预测策略。
  神经学和生物学的理论，如CPG。
######1.2.2运动控制
* transfers the
desired behavior into high-level actuator commands such as joint torque or position demand signals.
  虚拟模型控制VMC。作用在物体上的虚拟力分布到不同的接触点，然后映射到各个关节扭矩。
  控制操作空间（OSC）：Using different control gains and priorities, it can be ensured that important or high precision   
   tasks are accurately executed while other less important tasks are only fulfilled as well as possible without impairing the ones with higher priority.
######1.2.3关节控制
* regulates each joint independently.
  对于传统的大减速比的执行器，由于摩擦和齿轮间隙，难以建模和补偿。（使用干扰观测器来补偿）
####大纲
  多基体的浮动基座建模；处理接触限制和碰撞；系统动力学的解析表示。
  硬件、实时仿真系统
  控制高柔顺的SEA，有优秀的力位控制表现。
  分层二次优化，分层控制，设置不同的优先级

####系统建模
  MBS（multi-body systems）多刚体系统；
  EOM（equations of motion）：处理足端接触约束和由此产生的反力-->运动平衡方程。
  处理接触状态的瞬时变化、冲击、能量损失。    
  运动平衡方程：
  ![](assets/markdown-img-paste-20200104191641430.png)
##### 1接触模型
##### 1.1柔性接触
  弹簧阻尼腿，接触力和刚度与阻尼的大小有关，也就和速度、位置有关
  ![](assets/markdown-img-paste-20200104194331235.png)
##### 1.2刚性接触
  ![](assets/markdown-img-paste-20200104194156515.png)
![](assets/markdown-img-paste-2020010419441738.png)
![](assets/markdown-img-paste-20200104194436725.png)
