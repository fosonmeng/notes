- 交(Intersection)：
  $$
  R \cap S = \{ t | t \in R \land t \in S \}
  $$
- 连接(Join)：
	- \( \theta \) 连接
	  $$
	  R \underset{X \theta Y}{\Join} S = \{t | t=\langle t^n, t^m\rangle \land t^n \in R \land t^m \in S \land t^n[X] \theta t^m[Y] \}
	  $$
	  其中，\( X \theta Y \) 为连接的条件，\( \theta \) 是比较运算符，X和Y分别为R和S上度数相等，且可比的属性组。\( t^n[X] \) 表示R中\( t^n \) 元组的相应于属性X的一个分量。\( t^m[Y] \) 表示S中 \( t^m \) 元组的相应于属性Y的一个分量。
		- 或者也可以表示为：
		  $$
		  R \underset{i \theta j}{\Join} S = \{ t| t = \langle t^n, t^m \rangle \land t^n \in R \land t^m \in S \land t^n[i] \theta t^m[j] \}
		  $$
		- 由基本的关系运算笛卡尔积和选取运算导出：
		  \( R \underset{X \theta Y}{\Join} S = \sigma_{X \theta Y}(R \times S) \) 或 \( R \underset{i \theta j}{\Join} S = \sigma_{i \theta (i + j)}(R \times S) \)
		- ![image-20210818153109972](https://img.mhugh.net/typora/image-20210818153109972.png)
	- 等值连接：
	  $$
	  R \underset{X = Y}{\Join} S = \{ t| t = \langle t^n,t^m \rangle  \land t^n \in R \land t^m \in S \land t^n[X] = t^m[Y] \}
	  $$
	- 自然连接：
		- 是一种特殊的等值连接，它要求两个关系中==进行比较的分量必须是相同的属性组==，并且在结果集中将重复属性列去掉。若 \( t^n \) 表示R关系的元组变量，\( t^m \) 表示S关系的元组变量；R和S具有相同的属性组B，且`B=(B1,B2,…,Bk)`；并假定R关系的属性为`A1,A2,…,An-k,B1,B2,…,Bk`，S关系的属性为`B1,B2,…,Bk,Bk+1,BK+2,…,Bm`；为S的元组变量 \( t^m \) 去掉重复属性B所组成的新的元组变量为 \( t^{m^*} \) 。
		- 自然连接可以记为 \( R \Join S \)，其形式定义如下：
		  $$
		  R \Join S = \{ t | t = \langle t^n,t^m \rangle \land t^n \in R \land t^m \in S \land R.B_1 = S.B_1 \land R.B_2 = S.B_2 \land ... \land R.B_k = S.B_k \}
		  $$
		- 自然连接可以由基本的关系运算**笛卡尔积**和**选取运算**导出：
		  $$
		  R \Join S = \Pi_{A_a,A_2,...,A_{n-k},R.B_1,R.B_2,...,R.B_K,B_K,B_{K+1},B_{K+2},...,B_m}(\sigma_{R.B_1=S.B_1\land R.B_2=S.B_2\land...\land R.B_k=S.B_k}(R \times S))
		  $$
		- 特别需要说明的是，一般连接是从关系的水平方向运算，而自然连接不仅要从关系的水平方向，而且要从关系的垂直方向运算。因为自然连接要去掉重复属性，如果没有重复属性，那么自然连接就转化为笛卡尔积。
		- ![image-20210818160241025](https://img.mhugh.net/typora/image-20210818160241025.png)
		  ![image-20210818160311235](https://img.mhugh.net/typora/image-20210818160311235.png)
- 除(Division)：
	- 除运算是同时从关系的水平方向和垂直方向进行运算。给定关系R(X,Y)和S(Y,Z)，X、Y、Z为属性组。\( R \div S \)  应当满足元组在X上的分量值x的象集Yx包含关系S在属性组Y上投影的集合。其形式定义如下：
	  $$
	  R \div S = \{ t^n [X]| t^n \in R \land \pi_y(S) \subseteq Y_x \}
	  $$
	  其中，Yx为x在R中象集，\( x=t^n [X] \)。且 \( R \div S \)的结果集的属性组为X。
	- ![image-20210818170027507](https://img.mhugh.net/typora/image-20210818170027507.png)
- 广义投影(Generalized Projection)：广义投影运算允许在投影列表中使用算术运算，实现了对投影运算的扩充。
	- 若有关系R，条件F1,F2,…,Fn中的每一个都是涉及R中常量和属性的算术表达式，那么广义投影运算的形式定义如下：
	  $$
	  \pi_{F_1,F_2,...,F_n}(R)
	  $$
	- ![image-20210818172143721](https://img.mhugh.net/typora/image-20210818172143721.png)
- 外连接(Outer Join)：
	- 左外连接：取出左侧关系中所有与右侧关系中任一元组都不匹配的元组，用空值null充填所有来自右侧关系的属性，构成新的元组，将其加入**自然连接**的结果中。
	- 右外连接：取出右侧关系中所有与左侧关系中任一元组都不匹配的元组，用空值null充填所有来自左侧关系的属性，构成新的元组，将其加入**自然连接**的结果中。
	- 全外连接：完成左外连接和右外连接的操作。即填充左侧关系中所有与右侧关系中任一元组都不匹配的元组，又填充右侧关系中所有与左侧关系中任一元组都不匹配的元组，将产生的新元组加入**自然连接**的结果中。