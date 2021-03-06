- 最优二叉树：
	- 最优二叉树又称为**哈夫曼树**，是一类带权路径长度最短的树。路径是从树中一个节点到另一个节点之间的通路，路径上的分支数目称为路径长度。
	- 树的路径长度是从树根到每一个叶子之间的路径长度之和。节点的带权路径长为从该节点到树根之间的路径长度与该节点权的乘积。
	- 树的带权路径长度为树中所有叶子节点的带权路径长度之和，记为
	  $$
	  WPL = \Sigma_{k=1}^n w_k l_k
	  $$
	  其中，n为带权叶子节点数目，wk为叶子节点的权值，lk为叶子节点到根的路径长度。
	- 哈夫曼树是指权值为w1，w2，…，wn的n个叶子节点的二叉树中带权路径长度最小的二叉树。
	  ![image-20210830140738696](https://img.mhugh.net/typora/image-20210830140738696.png)
	- 那么如何构造一个最优二叉树呢？构造最优二叉树的哈夫曼算法如下。
	  1. 根据给定的n个权值{w1, w2, …, wn}，构成n棵二叉树的集合F={T1,T2, …, Tn}，其中每棵树Ti中只有一个带权为wi的根节点，其左右子树均空。
	  2. 在F中选取两棵权值最小的树作为左、右子树构造一棵新的二叉树，置新构造二叉树的根节点的权值为其左、右子树节点的权值之和。
	  3. 从F中删除这两棵树，同时将新得到的二叉树加入到F中。
	  4. 重复（2）、（3）步，直到F中只含一棵树时为止，这棵树便是最优二叉树（哈夫曼树）。
	- 由此算法可知，以选中的两棵子树构成新的二叉树，谁作为左子树，谁作为右子树，并没有明确。所以具有n个叶子节点的权值为w1，w2，…，wn的最优二叉树不唯一，但其WPL值是唯一确定的。
	- 当给定了n个权值后，构造出的最优二叉树中的节点数目m就确定了，即m=2xn-1，所以可用一维的结构数组来存储最优二叉树，下面举例说明。
	  ```c
	  #define MAXLEAFNUM 50
	  struct node {
	    char ch;
	    int weight;
	    int parent;
	    int lchild, rchild;
	  } HuffmanTree[2*MAXLEAFNUM];
	  typedef char* HuffmanCode[MAXLEAFNUM+1];
	  ```
	- 创建最优二叉树
	  ```c
	  void createHTree(HuffmanTree HT, char *c, int *w, int n) {
	    int i, s1, s2;
	    if (n <=1) reutrn;
	    for (i=0; i<=n; i++) { /* 根据n个权值构造n棵只有根节点的二叉树 */
	      HT[i].ch = c[i-1]; HT[i].weight = w[i-1];
	      HT[i].parent = HT[i].lchild = HT[i].rcihld = 0;
	    }
	    for (;i<2*n;i++) { /* 初始化 */
	      HT[i].parent = 0; HT[i].lchild = 0; HT[i].rchild = 0;
	    }
	    for(i = n+1; i<2*n;i++) {
	      /* 从 HT[1..i-1]中选择parent为0且weight最小的两棵树，其序号为s1和s2 */
	      select(HT, i-1, s1, s2);
	      HT[s1].parent = i; HT[s2].parent = i;
	      HT[i].lchild = s1; HT[i].rchild = s2;
	      HT[i].weight = HT[s1].weight + HT[s2].weight;
	    }
	  }
	  ```
- **哈夫曼编码**：
	- 若对每个字符编制相同长度的二进制码则称为等长编码。例如，英文字符集中的26个字符可采用5位二进制串表示，按等长编码格式构造一个字符编码表。发送方按照编码表对信息原文进行编码后送出电文，接收方收到的二进制代码按每5位一组进行分割，通过查字符的编码表即可得到对应字符，实现译码。
	- 等长编码方案的实现方法比较简单，但对通信中的原文进行编码后，所得电文的码串过长，不利于提高通信效率，因此希望缩短码串的总长度。如果对每个字符设计长度不等的编码，且让电文中出现次数较多的字符采用尽可能短的编码，那么传送的电文码串总长度则可减少。
	- 要设计长度不等的编码，必须满足下面的条件：任一字符的编码都不是另一个字符的编码的前缀，这种编码也称为**前缀码**。对给定的字符集D={d1,d2,…,dn}及字符的使用频率W={w1,w2,…,wn}，构造其最优前缀码的方法为：以d1,d2,…,dn作为叶子节点，w1,w2,…,wn作为叶子节点的权值，构造出一棵最优二叉树，然后将树中每个节点的左分支标上0，右分支标上1，则每个叶子节点代表的字符的编码就是从根到叶子的路径上的0、1组成的串。最优前缀编码方法如图8-24。
	  ![image-20210830145231272](https://img.mhugh.net/typora/image-20210830145231272.png)
	- 从每个叶子节点出发追溯到树根，逆向找出最优二叉树中叶子节点的编码
	  ```c
	  void HuffmanCoding(HuffmanTree HT, HuffmanCode HC, int n) {
	    char *cd; inti, start, c, f;
	    if (n <= 1) return;
	    cd = (char *) malloc(n); cd[n-1] = '\0';
	    for (i = 1; i<=n; i++) {
	      start = n -1;
	      for (c=i,f=HT[i].parent; f!=0;c=f,f=HT[f].parent)
	        if (HT[f].lchild == c) cd[--start] = '0';
	      	else cd[--start]='1';
	      HC[i] = (char*) malloc(n-start);
	      strcpy(HC[i], &cd[start]);
	    }
	    delete cd;
	  }
	  ```
	- 利用哈夫曼树译码的过程为：从根节点出发，按二进制位串中的0和1确定是进入左分支还是右分支，当到达叶子节点时译出一个字符。若位串未结束，则回到根节点继续上述译码过程。
	  ```c
	  void Decoding(HuffmanTree HT, int n, char *buff) {
	    int p = 2*n-1;
	    while (*buff) {
	      if ((*buff) == '0') p = HT[p].lchild;
	      else p = HT[p].rchild;
	      if (HT[p].lchild == 0 && HT[p].rchild == 0) {
	        printf("%c", HT[p].ch);
	        p = 2*n -1; /* 回到树根 */
	      }
	      buff++;
	    }
	  }
	  ```