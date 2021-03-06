- 问题的解空间：
	- 应用回溯法解问题时，首先应明确定义问题的解空间。问题的解空间应至少包含问题的一个（最优）解。例如，对于有n种可选择物品的0-1背包问题，其解空间由长度为n的0-1向量组成。该解空间包含了对变量的所有可能的0-1赋值。当n=3时，其解空间是{(0,0,0),(0,1,0),(0,0,1),(1,0,0),(0,1,1),(1,0,1),(1,1,0),(1,1,1)}。
	- 定义了问题的解空间后，还应将解空间很好地组织起来，使得用回溯法能方便地搜索整个解空间。通常将解空间表示为树或图的形式。例如，对于n=3时的0-1背包问题，其解空间用一棵完全二叉树表示，如图9-7所示。
	  ![image-20211014180005226](https://img.mhugh.net/typora/image-20211014180005226.png)
	- 解空间树的第i层到第i+1层边上的标号给出了变量的值。从树根到叶子的任一路径表示解空间的一个元素。例如，从根节点到节点H的路径对应于解空间中的元素(1,1,1)。
- 回溯法的基本思想：
	- 确定了解空间的组织结构后，回溯法从开始节点（根节点）出发，以深度优先的方式搜索整个解空间。这个开始节点就成为一个活节点，同时也成为当前的扩展节点。在当前的扩展节点处，搜索向纵深方向移至一个新节点。这个新节点就成为一个新的活节点，并成为当前扩展节点。如果在当前扩展节点处不能再向纵深方向移动，则当前的扩展节点就成为死节点。换句话说，这个节点不再是一个活节点。此时，应往回移动（回溯）至最近的一个活节点处，并使这个活节点成为当前的扩展节点。回溯法即以这种工作方式递归地在解空间中搜索，直至找到所要求的解或解空间中已无活节点为止。
	- 例如，对于n=3时的0-1背包问题，考虑下面的具体实例：w=[16,15,15]，p=[45,25,25]，c=30。其中w表示物品的重量，p表示物品的价值，c表示背包能够容纳的最大重量。从图9-7的根节点开始搜索其解空间。
		- 开始时根节点是唯一的活节点，也是当前的扩展节点。在这个扩展节点处，按照深度优先策略移至节点B或节点C。假设选择先移至节点B。此时节点A和节点B是活节点，节点B成为当前的扩展节点。由于选取了w1（节点A到B的边上标记为1，表示选择物品），故在节点B处剩余背包容量是r=14，获取的价值是45。
		- 从节点B处可以移至节点D或E。由于移至节点D需要w2=15的背包容量，而现在的背包容量是r=14，故移至节点D导致一个不可行的解。而搜索至节点E不需要占用背包容量（节点B到节点E的边上标记为0，表示不需要选择物品），因而是可行的。从而选择移至节点E。此时，E成为新的扩展节点，节点A、B和E 是活节点。在节点E处，r=14，获取的价值为45。
		- 从节点E处可以移至节点J或K。移至节点导致一个不可行解，而移至节点K是可行的，于是移至节点K，它成为一个新的扩展节点。由于节点K是一个叶节点，故得到一个可行解，这个解对应的价值为45。解x的取值是由根节点到叶节点K的路径所唯一确定，即x=(1,0,0)。由于在节点K处已不能再向纵深扩展，所以节点K成为死节点。返回到节点E，此时在E处也没有可扩展的节点，它也成为一个死节点。
		- 返回节点B处，节点B同样也成为死节点，从而节点A再次成为当前扩展节点。节点A还可以继续扩展，从而达到节点C。此时r=30，获取的价值为0。
		- 从节点C可移至节点F或G。假设移至节点F，它成为新的扩展节点。节点A、C和F 是活节点。在节点F处，r=15，获取的价值为25。从节点F移至节点L处，此时r=0，获取的价值为50。由于L是一个叶节点，而且是迄今为止找到的获取价值最高的可行解，因此记录这个可行解。节点L不可扩展，返回到节点F处。
	- 按此方式继续搜索，可搜索整个解空间。搜索结束后找到的最好解就是0-1背包问题的最优解。
	- 综上所述，运用回溯法解题通常包含以下三个步骤。
	  1. 针对所给问题，定义问题的解空间。
	  2. 确定易于搜索的解空间结构。
	  3. 以深度优先的方式搜索解空间。
- 回溯法的算法框架：
	- 回溯法的算法框架有非递归和递归两种方式。
	- 非递归方式：
	  ```c
	  BackTracking(X)
	    计算解X的第一个元素的候选集合S
	    k <- 1
	    while k >0 do
	      while Sk != \Phy do
	        xk <- Sk中的下一个元素
	        Sk <- Sk-{xk}
	  			if X = {x1,x2,...,xk}是问题的解
	    			then 输出 X
	        k <- k+1
	        计算解X的第k个元素的候选集合Sk
	          k <- k-1
	    return
	  ```
	- 递归方式：
	  ```c
	  BackTrackingDFS(X,k)
	    if X=(x1,x2,...,xk)是问题的解
	      then 输出 X
	      else k <- k+1
	        计算解X的第k个元素的候选集合Sk
	        while Sk != \Phy do
	          xk <- Sk中的下一个元素
	          Sk <- Sk-{xk}
	  				BackTrackingDFS(X,k)
	    return
	  ```
- 回溯法的限界函数：
	- 问题的解空间往往很大，为了有效地进行搜索，需要在搜索的过程中对某些节点进行剪枝。而对哪些节点进行前传，需要设计限界函数来判断。因此，限界函数的设计是回溯法的一个核心问题，也是一个很难的问题。设计限界函数的通用的指导原则是尽可能多和尽可能早地“杀掉”不可能产生最优解的活节点。好的限界函数可以大大减少问题的搜索空间，从而大大提高算法的效率。下面通过例子说明。