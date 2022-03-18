- 计算机系统结构概述：
	- 体系结构：
	- 组织：逻辑实现
	- 实现：物理实现
- 计算机体系结构分类：
	- 处理机数量： ![](http://www.plantuml.com/plantuml/svg/SoWkIImgoStCIybDBE3Yqb9ukgJb-OIsPtDsFP_LycpgXfVj_LnQMl4AJtkdGcIURzxzVFTyYDZERIyMza24d-peUxfa5gQIZhQdEvgVxkb7aN581Le7jH80)
	- 并行程度：
		- Flynn分类法：按指令流和数据流的多少 ![](http://www.plantuml.com/plantuml/svg/SoWkIImgoStCIybDBE3Yqb9mowdCotlQqVPyu-vdcwToQMd5AmHx1hj06RuGXYzCn1Sauf0Ar0qr0G00)
- 指令系统：
	- 指令集体系结构： ![](http://www.plantuml.com/plantuml/svg/SoWkIImgoStCIybDBE3Yqb9urjF-PFUIbxFRdkoT_7ppxkUx9p-RryAbfHMly6noxvEzSvvDtV1qpWhdWD0dEzO-dzNoTEsCfqqhdatR-NHFFqJLZ7r09bmjK0cGVDdUZse4KFZ9tjxdUzT1XC5sWfI2vJ6KFj-u--cyxYSx-fukMVvqGp-NGohGkL0d0m00)
		- TODO 堆栈、累加器、寄存器集：
		- TODO 通用寄存器&GPR机：
		- 指令格式及其优化：指令长度、是否有足够空间表示所有期望的操作、存取指令速度的提高及寻址字段长度的选择
	- #CISC和RISC
	- 指令的流水处理：
		- 指令控制方式：
			- 顺序方式：
			- 重叠方式：
			- 流水方式： ![47bf8690a2f2ccbfb27c0b41155cc9d4.png](https://img.mhugh.net/typora/2303a4c2f36a4e51a7e539dd2cd65f48.png)
		- TODO 流水线种类：
		- TODO 流水的相关处理：
			- RISC #CISC和RISC 中采用的流水技术：
			  > 1. 超流水线技术
			  > 2. 超标题技术
			  > 3. 超长指令字段技术
		- 吞吐率和流水建立时间：
			- 最大吞吐率：
			  $$
			  p = 1/max\{\Delta t_1,\Delta t_2,...,\Delta t_m\}
			  $$
- 阵列处理机、并行处理机和多处理机：
	- **同时性**：两个或两个以上的事件在同一时刻发生；**并发性**：两个或两个以上的事件在同一时间间隔内连续发生
	- 计算机信息处理的步骤和阶段的角度看，并行处理分为：
	  > 1. 存储器操作并行
	  > 2. 处理器操作步骤并行（流水线处理机）
	  > 3. 处理器操作并行（阵列处理机）
	  > 4. 指令、任务、作业并行（多处理机、分布处理系统、计算机网络）
	- **阵列处理机**：处理单元PU，单个控制部件CU。
	  单指令流多数据流计算机，通过资源重复实现并行性
	- **并行处理机**：SIMD和MIMD。
	  互联网络ICN，处理单元PE，控制部件CU，共享存储器M，局部存储器PEM。 ![1f52167a6a856db7ef3c688705424673.png](https://img.mhugh.net/typora/494ec77bf5ea425aa76487d2b43a4e7d.png)
	- 多处理机：机间的互联技术决定着多处理机的性能。
	  高频带、低成本、连接方式的多样性以及在不规则通信情况下连接的无冲突性。
	- 其他计算机： #集群 ； #网格计算 ；