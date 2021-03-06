- 【例9.7】归并排序。
  归并排序算法是成功应用分治法的一个完美的例子，其基本思想是将待排序元素分成大小大致相同的两个子序列，分别对这两个子序列进行排序，最终将排好序的子序列合并为所要求的序列。归并排序算法完全依照上述分治算法的三个步骤进行。
  1. 分解。将n个元素分成各含n/2个元素的子序列。
  2. 求解。用归并排序对两个子序列递归地排序。
  3. 合并。合并两个已经排好序的子序列以得到排序结果。
- 归并排序算法的伪代码如下：
  ```c
  MergeSort(A,p,r)
  	if p < r
      then q <- (p+r)/2
      	MergeSort(A,p,q)
      	MergeSort(A,q+1,r)
      	Merge(a,p,q,r)
  ```
  过程Merge(A,p,q,r)的伪代码为：
  ```c
  Merge(A,p,q,r)
    n1 <- q-p+1 and n2 <- r-q
    create arrays L[1..n1+1] and R[1..n2+1]
    for i <- 1 to n1
      do L[i] <- A[p+i-1]
    for j <- 1 to n2
      do R[j] <- A[q+j]
    L[n1+1] <- \infty and R[n2+1] <- \infty
    i <- 1 and j <- 1
    for k <- p to r
      do if L[i] <= R[j]
        then A[k] <- L[i] and i <- i+1
        else A[k] <- R[j] and j <- j+1
  ```
- 其中，A是数组，p、q和r是下标，满足p<=q<r。Merge显然可在O(n)时间内完成，因此合并排序算法对n个元素进行排序所需的计算时间T(n)满足：
  $$
  T(n) = \begin{cases}
  O(1) & n \le 1 \\
  2T(n/2) + O(n) & n > 1
  \end{cases}
  $$
  解此递归式可知T(n)=O(n\log n)。
- 【例9.8】最大子段和问题。
  给定由n个整数（可能有负整数）组成的序列a1,a2,…,an，求该序列形如$$\Sigma_{k=i}^{j} a_{k}$$ 的子段和的最大值。当序列中所有整数均为负整数时，其最大子段和为0。依此定义，所求的最优值为
  $$
  \max\{0, \max_{l \le i \le j \le n} \sum_{k=i}^{j} a_{k}\}
  $$
  例如，当(a1,a2,a3,a4,a5,a6)=(-2,11,-4,13,-5,-2)时，最大子段和为 $$\sum_{k=2}^{4} a_{k} = 20$$。
- 最大子段和问题的分治策略如下。
	- 分解。如果将所给的序列A[1..n]分为长度相等的两段A[1..n/2]和A[n/2+1..n]，分别求出这两段的最大子段和，则A[1..n]的最大子段和有三种情形。
	  1. A[1..n]的最大子段和与A[1..n/2]的最大子段和相同。
	  2. A[1..n]的最大子段和与A[n/2+1..n]的最大子段和相同。
	  3. A[1..n]的最大子段和为$$\Sigma_{k=i}^{j} a_{k}$$，且 1<=i<=n/2，n/2+1<=j<=n。
	- 解决。1和2这两种情形可递归求得。对于情形3，容易看出，A[n/2]与A[n/2+1]在最优子序列中。因此可以在A[1..n/2]中计算出$$s1=max_{1 \le i \le n/2} \Sigma_{k=i}^{n/2} a[k]$$，并在A[n/2+1..n]中计算出$$s2=max_{n/2+1 \le i \le n} \Sigma_{k=n/2}^{i} a[k]$$。遇s1+s2即为出现情形3的最优值。
	- 合并。比较在分解阶段的三种情况下的最大子段和，取三者之中的较大者为原问题的解。
- 据此可设计出求解最大子段和的分治算法如下：
  ```c
  MaxSum(A,n)
    return MaxSubSum(A,1,n)
  ```
  过程MaxSubSum(A,1,n)的伪代码为：
  ```c
  MaxSubSum(A,left,right)
    sum <- 0
    if left = right
      then if A[left] > 0
        then sum <- A[left]
        else sum <- 0
      else center <- (left+right)/2
        leftsum <- MaxSubSum(A,left,center)
        rightsum <- MaxSubSum(A,center+1,right)
        s1 <- 0
        lefts <- 0
        for i <- center downto left
          do lefts <- lefts+A[i]
            if lefts > s1
              then s1 <- lefts
        s2 <- 0
        rights <- 0
        for i <- center+1 to right
          do rights <- rights+A[i]
            if rights > s2
              then s2 <- rights
        sum <- s1+s2
        if sum < leftsum
          then sum <- leftsum
        if sum < rightsum
          then sum <- rightsum
    return sum
  ```
- 其中A为数组，left和right表示数组下标。对应分解中的1和2两种情形，需要分别递归求解，对应情形3，两个并列for循环的时间复杂度为O(n)，因此得到下列递归式。
  $$
  T(n)=\begin{cases}
  O(1) & n<=1 \\
  2T(n/2)+O(n) & n>1 
  \end{cases}
  $$
  解此递归式可知T(n)= O(n\log n)。
- 【例9.9】循环赛日程安排。
  设有 \( n(2^k) \) 位选手参加网球循环赛，循环赛共进行n-1天，每位选手要与其他n-1位选手赛一场，且每位选手每天赛一场，不轮空。试按此要求为比赛安排日程。
  设n位选手被顺序编号为1，2，…，n。比赛的日程是一个n行n-1列的表，第i行j列的内容是第i号选手第j天的比赛对手。用分治法设计日程表，就是从其中一半选手(\( 2^{k-1} \)位)的比赛日程导出全体(\( 2^k \)位)选手的比赛日程。从众所周知的只有两位选手的比赛日程出发，反复这个过程，直至为n位选手安排好比赛日程为止。
  为了从\( 2^{k-1} \)位选手的比赛日程表中导出 \( 2^k \) 位选手的比赛日程表，假定只有8位选手（如图9-3所示），若1\~4号选手之间的比赛日程填在日程表的左上角（4行3列），5\~8号选手之间的比赛日程填在日程表的左下角(4行3列)，而左下角的内容可以由左上角对应项加上数4得到。至此，剩下的右上角（4行4列）是为编号小的1\~4号选手与编号大的5\~8号选手之间的比赛安排日程。例如在第4天，让1\~4号选手分别与5\~8号选手比赛，以后各天，依次由前一天的日程安排，让5\~8号选手循环轮转即可。最后，参照右上角得到右下角得到右下角的比赛日程，如图9-3所示。由以上分析，不难得到为 \( 2^k\) 选手安排比赛的算法思路。
  ![image-20211013080530679](https://img.mhugh.net/typora/image-20211013080530679.png)
- 循环赛日程安排算法的关键在于寻找这4部分元素之间的对应关系，其伪代码如下：
  ```c
  GameTable(A,k)
    n <- 2
    A[1][1] <- 1
    A[1][2] <- 2
    A[2][1] <- 2
    A[2][1] <- 1
    for t <- 1 to k-1
      do temp <- n
        n <- n*2
      for i <- temp + 1 to n
        do for j <- 1 to temp
          do A[i][j] <- A[i-temp][j] +temp
      for i <- 1 to temp
        do for j <- temp+1 to n
          do A[i][j] <- A[i+temp][(j+temp)%n]
      for i <- temp+1 to n
        do for j <- temp+1 to n
          do A[i][j] <- A[i-temp][j-temp]
  ```
  其中A为数组，\( n=2^k \) 表示参加比赛的人数。