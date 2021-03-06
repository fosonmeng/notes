- 选择调度算法需要考虑的因素：与系统的整个设计目标一致，均衡使用系统资源，以及平衡系统和用户的要求。对用户来说，作业能“立即执行”往往难以做到，但是应保证进入系统的作业在规定的截止时间内完成，而且系统应设法缩短作业的平均周转时间。
- 作业调度算法：
	- **先来先服务**。按作业到达先后进行调度，即启动等待时间最长的作业。
	- **短作业优先**。以要求运行时间长短进行调度，即启动要求运行时间最短的作业。
	- **响应比高优先**。响应比高的作业优先启动。
	  定义响应比 $$R_{p} = \frac{作业响应时间}{作业执行时间}$$
	  其中**作业响应时间**为作业进入系统后的等候时间与作业的执行时间之和，即$$R_{p}=1+\frac{作业等待时间}{作业执行时间}$$。
	  响应比高者优先算法，在每次调度前都要计算所有被选作业（在作业后备队列中）的响应比，然后选择响应比最高的作业执行。该算法比较复杂，系统开销大。
	- **优先级调度算法**。可由用户指定作业优先级，优先级高的作业先启动。也可由系统根据作业要求的紧迫程序，或者照顾“I/O繁忙”的作业，以便充分发挥外设的效率等。
	- **均衡调度算法**。这种算法的基本思想是根据系统的运行情况和作业本身的特性对作业进行分类。作业调度程序轮流地从这些不同类别的作业中挑选作业执行。这种算法力求均衡地使用系统的各种资源，即注意发挥系统效率，又使用户满意。
- 作业调度算法性能的衡量指标：
	- 在一个以批量处理为主的系统中，通常用**平均周转时间**或**平均带权周转时间**来衡量调度性能的优劣。假设作业`Ji(i=1,2,…,n)`的提交时间为`tsi`，执行时间为`tri`，作业完成时间为`toi`，则作业`Ji`的周转时间`Ti`和带权周转时间`Wi`分别定义为：
	  $$
	  T_{i} = t_{oi} - t_{si}  \; (i = 1,2,...,n) \\
	  W_{i} = T_{i}/t_{ri}  \; (i = 1,2,...,n)
	  $$
	  n个作业的平均周转时间`T`和平均带权周转时间`W`分别为：
	  $$
	  T = \frac{1}{n}\Sigma^{n}_{i=1}T_{i} \\
	  W = \frac{1}{n}\Sigma^{n}_{i=1}W_{i}
	  $$
	- 站在用户的角度来说，总是希望自己的作业在提交后能立即执行，这意味着当等待时间为0时作业的周转时间最短，即`Ti=tri`。但是，作业的执行时间`tri`并不能直观地衡量出系统的性能，而带权周转时间`Wi`却能直观反映系统的调度性能。站在整个系统的角度来说，不可能满足每个用户的这种要求，而只能是系统的平均周转时间或平均带权周转时间最小。