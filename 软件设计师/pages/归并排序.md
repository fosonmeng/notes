- 所谓“归并”，是将两个或两个以上的有序文件合并成为一个新的有序文件。归并排序是把一个有n个记录的无序文件看成是由n个长度为1的有序文件组成的文件，然后进行两两归并，得到\ceiling{n/2}个长度为2或1的有序文件，再两两归并，如此重复，直至最后形成包含n个记录的有序文件为止。这种反复将两个有序文件归并成一个有序文件的排序方法称为两路归并排序。
- 两路归并排序的核心操作是将一维数组中前后相邻的两个有序序列归并为一个有序序列。
- 【算法】将分别有序的data1[s..m]和data1[m+1..n]归并为有序的data2[s..n]。
  ```c
  void Merge(int data1[], int data2[], int s, int m, int n)
  {
    int i,k;
    for(i=m+1,k=s;s<=m && i<=n;++k) /* 将data1中记录由小到大地并入data2 */
      if(data1[s] < data1[i]) data2[k] = data1[s++];
    	else data2[k] = data1[i++];
    for(;s<=m;++k) /* 将剩余的data1[s..m]复制到data2 */
      data2[k] = data1[s++];
    for(;i<=n;++k) /* 将剩余的data1[i..n]复制到data2 */
      data2[k] = data1[i++];
  }
  ```
- 一趟归并排序的操作是：调用 \( \lceil n/2h \rceil \) 次Merge算法，将数组data1[0..n-1]中前后相邻且长度为h的有序段进行两两归并，得到前后相邻、长度为2h的有序段，并存放在data2[0..n-1]中，整个归并排序需进行\( \lceil \log_{2} n \rceil \) 趟。可见，归并排序需要辅助空间n个（与待排记录数量相等），时间复杂度为 \( O(n \log n) \)。
- 【算法】递归形式的两路归并。
  ```c
  void MSort(int data1[], int data2[], int s, int t) /* 将data[s..t]归并排序为data2[s..t] */
  { int m, *temp;
    if (s == t) data2[s] = data1[s];
    else {
      temp = (int *)malloc((t-s+1)*sizeof(int)); /* 辅助空间 */
      m = (s+t)/2; /* 将data1[s..t]均分为data1[s..m]和data1[m+1..t] */
      MSort(data1, temp, s, m); /* 递归地将data1[s..m]归并为有序的temp[s..m] */
      MSort(data1, temp, m+1, t); /* 递归地将data1[m+1..t]归并为有序的temp[m+1..t] */
      Merge(temp, data2, s, m, t); /* 将temp2[s..m]和temp2[m+1..t]归并到data2[s..t] */
      free(temp);
    }
  }
  ```
- 【算法】对一维数组data1[0..n-1]中的元素进行两路归并排序。
  ```c
  void MergeSort(int data1[], int n)
  {
    MSort(data1, data1, 0, n-1);
  }
  ```