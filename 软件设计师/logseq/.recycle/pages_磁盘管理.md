- 磁盘是可被多个进程共享的设备。当有多个进程请求访问磁盘时，为了保证信息的安全，系统每一时刻只允许一个进程启动磁盘进行I/O操作，其余的进程只能等待。因此，操作系统应采用一种适当的调度算法，使各进程对磁盘的平均访问（主要是**寻道**）时间最小。磁盘调度分为移臂调度和旋转调度两类，并且时先进行==移臂调度==，然后进行==旋转调度==。由于访问磁盘最耗时的是寻道时间，因此，磁盘调度的目标是使磁盘的平均寻道时间最少。
- 磁盘驱动调度： _磁盘调度在多道程序设计的计算机系统中，各个进程可能会不断提出不同的对磁盘进行读/写操作的请求。由于有时候这些进程的发送请求的速度比磁盘响应的还要快，因此我们有必要为每个磁盘设备建立一个等待队列。我们不妨将磁道由内向外进行编号 1，2，3...n。_
	- ==先来先服务==FCFS：这种算法最公平，谁先来谁就先被服务。但是相应地，其可能会出现排在后面的进程长期无法得到满足。另外，假如先来一个 1 号磁道的请求，然后是 n 号，然后又 1 号，这样效率就会很低，我们先处理完成 1 号的两个请求，再处理最号，实际上这就是我们接下来要讲的 SSTF（最短寻道时间优先）。
	- ==最短寻道时间优先== SSTF Shortest-seek-time First：选择使磁头从当前位置开始移动最少的磁盘I/O请求，所以 SSTF 总是选择导致最小寻道时间的请求。总是选择最小寻找时间并不能保证平均寻找时间最小，但是能提供比 FCFS 算法更好的性能，会存在饥饿现象。
	- ==扫描算法== SCAN：这种算法是在 SSTF（最短寻道时间优先）的基础上，我们增加一个考虑因素`当前磁头移动的方向`。例如，当磁头正在自里向外移动时，扫描算法所选择的下一个访问对象应是其欲访问的磁道既在当前磁道之外，又是距离最近的。这样自里向外地访问，直到再无更外的磁道需要访问才将磁臂换向，自外向里移动。
		- SSTF+中途不回折，每个请求都有处理机会。
		- SCAN 要求磁头仅仅沿一个方向移动，并在途中满足所有未完成的请求，直到它到达这个方向上的最后一个磁道，或者在这个方向上没有其他请求为止。
		- 由于磁头移动规律与电梯运行相似，SCAN 也被称为电梯算法。
		- SCAN 算法对最近扫描过的区域不公平，因此，它在访问局部性方面不如 FCFS 算法和 SSTF 算法好。
	- ==单向扫描调度算法==：
	- ==循环扫描== CSCAN：实际上，当我们从 1 号磁道，到达 n 号磁道的时候，这个时候 1 号磁道的请求应该会很多，因为我们刚刚响应过了 n 号磁道，其 n-1，n-2 相对来说请求比 1，2，3... 请求少。为了解决这个问题就发明了 CSCAN（循环扫描）。循环扫描算法规定磁头单向移动。例如，只自里向外移动，当磁头移到最外的被访问磁道时，磁头立即返回到最里的欲访磁道，即将最小磁道号紧接着最大磁道号构成循环，进行扫描。
		- SCAN+直接移到另一端，两端请求都能很快处理。
		- 把扫描限定在一个方向，当访问到某个方向的最后一个磁道时，磁道返回磁盘相反方向磁道的末端，并再次开始扫描。
		- 其中“C”是Circular（环）的意思。
	- LOOK 和 C-LOOK：釆用SCAN算法和C-SCAN算法时磁头总是严格地遵循从盘面的一端到另一端，显然，在实际使用时还可以改进，即磁头移动只需要到达最远端的一个请求即可返回，不需要到达磁盘端点。这种形式的SCAN算法和C-SCAN算法称为LOOK和C-LOOK调度。这是因为它们在朝一个给定方向移动前会查看是否有请求。
- 旋转调度算法：
	- 当移动臂定位后，有多个进程等待访问该柱面时，就当如何决定这些进程的访问顺序？这就是旋转调度要考虑的问题。显然，系统应该选择延迟时间最短的进程对磁盘的扇区进行访问。当有若干等待进程请求访问磁盘上的信息时，旋转调度应考虑如下情况：
	  1. 进程请求访问的是同一磁道上不同编号的扇区
	  2. 进程请求访问的是不同磁道上不同编号的扇区
	  3. 进程请求访问的是不同磁道上具有相同编号的扇区
	- 对于 :one: 和 :two: ，旋转调度总是让首先到达读写磁头位置下的扇区先进行传送操作；对于:three: ，旋转调度可以任选一个读写磁头位置下的扇区进行传送操作。
- ```
  磁盘访问延迟 = 队列时间 + 控制器时间 + 寻道时间 + 旋转时间 + 传输时间
  ```
  磁盘调度的目的是减小延迟，其中前两项可以忽略，寻道时间是主要矛盾。
-