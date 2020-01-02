####Stanford 分层控制
*****
Mian：三层控制；静步态、COG规划   
#### 三层控制
![](assets/markdown-img-paste-20200102162226979.png)   
#####1 High-level Planner    
determine a set of feasible footsteps across the terrain.
Build “foot cost map”-->find the minimum cost set of footsteps-->average the foot costs,form a “body cost map”
######1.1.1 Generate height and collision maps of the terrain
生成三维网格化地图（离散化高度）。预计算合适的碰撞地图。
######1.1.2 Generate local features of the terrain
（对当前点5 7 11 21四种方格数量），计算1 x方向的斜度。2 y方向的斜度。 3 相对中心点的最大高度差。 4 相对中心点的最小高度差。 5 高度标准差。 一共20个数，构成一个20维的向量。
######1.1.3 Generate foot cost maps
用一个权重矩阵将1.1.2的参数线性结合。
Hierarchical Apprenticeship Learning (HAL)的方法来确定参数。
######1.1.4 Form body cost map and plan body path
######1.1.5. Plan footsteps along the desired body path
提前规划几步。
#####2 底层规划
2.1在上层规划中的身体路径是一个大致的路径。而在底层规划中的COG路径为重心的真实路径（保持平衡）。如下图所示，提前规划好了两步的重心。<font color=#FF0000 >取两个三角形的重合区域</font>保证了不会将重心后移
![](assets/markdown-img-paste-20200102184648428.png)    
其核心为：是COG点的移动距离最小。   、
足端轨迹用矩形（不用判断最高的障碍点在哪，省时）
#####3 底层控制
闭环控制机制-->防止打滑；  
1.稳定检测与恢复：
用状态估计来判断足端位置，实时计算稳定三角形。若发现打滑，则从新进行一次底层规划（只规划一步）。
2.身体稳定性：
![](assets/markdown-img-paste-20200102220706551.png)
取步长为0.1。
3.足端位置闭环：
防止由于身体位置不准导致的足端锤地。
#####4 实验
将身体重心移到稳定三角形中心时，增加了腿与障碍碰撞的可能性，因此在试验中效果不佳。
