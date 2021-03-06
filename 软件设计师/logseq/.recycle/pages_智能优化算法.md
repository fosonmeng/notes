- 智能优化算法概述：
	- 优化技术是一种以数学为基础，用于求解各种工程问题优化解的应用技术。作为一个重要的科学分支，它一直受到人们的广泛重视，并在诸多工程领域得到迅速推广和应用，如系统控制、人工智能、模式识别、生产调度、VLSI技术和计算机工程等。鉴于实际工程问题的复杂性、约束性、非线性、多极小、建模困难等特点，寻求一种适合于大规模并行且具有智能特征的算法已成为有关学科的一个主要研究目标和引人注目的研究方向。20世纪80年代以来，一些新颖的优化算法，如人工神经网络、混沌、遗传算法、进化规划、模拟退火、禁忌搜索及其混合优化策略等，通过模拟或提示某些自然现象或过程而得到发展，其思想和内容涉及数学、物理学、生物进化、人工智能、神经科学和统计力学等方面，为解决复杂问题提供了新的思路和手段。这些算法独特的优点和机制，引起了国内外学者的广泛重视并掀起了该领域的研究热潮，且在诸多领域得到的成功应用。在优化领域，由于这些算法构造的直观性与自然机理，因而通常被称作智能优化算法，或称现代启发式算法。
- 人工神经网络：
	- 人工神经网络（ANN）是一个以有向图为拓扑结构的动态系统，它通过对连续或断续的输入作状态响应而进行信息处理。人工神经网络技术与计算机技术的结合，为人类进一步研究模拟人类智能及了解人脑思维的奥秘开辟了一条新途径。
- 遗传算法：
	- 遗传算法是源于模拟达尔文的“优胜劣汰、适者生存”的进化论和孟德尔·摩根的遗传变异理论，在迭代过程中保持已有的结构，同时寻找更好的结构。其本意是在人工适应系统中设计一种基于自然的演化机制。
- 模拟退火算法：
	- 模拟退火算法（SA）是一种求解全局优化算法。模拟退火算法的基本思想来源于物理退火过程，所谓物理退火过程包括3个阶段。
	  1. 加温阶段。
	  2. 等温阶段。
	  3. 冷却阶段。
	- 模拟退火算法的思想是：先将固体加热至熔化，再让其徐徐冷却，凝固成规整晶体。在加热固体时，固体内部的粒子随着温度的升高，粒子排列从较有序的结晶状态转变为无序的液态，这个过程称为熔解，此时内能增大；冷却时，液体粒子随着温度的徐徐降低，粒子渐趋有序，液体凝固成固体的晶态，这个过程称为退火。最后在常温时达到基态，内能减为最小。
- 禁忌搜索算法：
	- 禁忌搜索算法（TS）是模拟人类智力过程的一种全局搜索算法，是对局部邻域搜索的一种扩展。禁忌包含两个方面的意思，一方面，当沿着产生相反结果的道路走下去时，也不会陷入一个圈套而导致无处可逃；另一方面，在必要情况下，保护措施允许被淘汰，也就是说，某种措施被强制运用时，禁忌条件就宣布无效。
- 蚁群算法：
	- 蚁群算法的原理：蚂蚁在寻找食物或者寻找回巢的路径中，会在它们经过的地方留下一些信息素，而信息素能被同一蚁群中后来的蚂蚁感受到，并作为一种信号影响后到者的行动（具体表现在后到的蚂蚁选择有信息素的路径的可能性，比选择没有信息素的路径的可能性大得多），而后到者留下的信息素会对的原有的信息素进行加强，并如此循环下去。这样，经过蚂蚁越多的路径，在后到蚂蚁的选择中被选中的可能性就越大（因为敖的信息素浓度较大）。由于在一定的时间内，越短的路径会被越多的蚂蚁访问，因而积累的信息素也就越多，在下一个时间内被其他的蚂蚁选中的可能性也就越大。这个过程会一直持续到所有的蚂蚁都走最短的那一条路径为止。这种行为表现出一种信息正反馈现象：某一路径上走过的蚂蚁越多，则后到者选择该路径的概率就越大，因此距离近的食物源会吸引越多的蚂蚁，信息素浓度的增长速度就会越快，同时通过这种信息的交流，蚂蚁也就寻找到食物与蚁穴之间的最短路径了。
- 粒子群优化算法：
	- 粒子群算法的基本思想：鸟群觅食飞行时，在飞行过程中经常会突然改变方向、散开、聚集，其行为不可预测，但其整体总保持一致性，个体与个体间也保持着最适宜的距离。通过对类似生物群体行为的研究，发现生物群体中存在着一种信息共享机制，罚群体的进化提供了一种优势，这就是基本粒子群算法形成的基础。