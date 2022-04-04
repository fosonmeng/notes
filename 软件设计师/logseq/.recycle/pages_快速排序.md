- 快速排序的基本思想是：通过一趟排序将待排的记录分割为独立的两部分，其中一部分记录的关键字均不大于另一部分记录的关键字，然后再分别对这两部分记录继续进行排序，以达到整个序列有序。
- 用一维数组存储记录，一趟快速排序的具体做法是：附设两个指针low和high，它们的初值分别指向第一个记录和最后一个记录。设枢轴记录（通常是第一个记录）的关键字为pivotkey，则首先从high所指位置起向前搜索，找到第一个关键字小于pivotkey的记录与枢轴记录互相交换，然后从low所指位置起向后搜索，找到第一个关键字大于pivotkey的记录与横轴记录互相交换，重复这两步直至low等于high时为止。
- 【函数】用快速排序方法对整型数组进行非递减排序。
  ```c
  void QuickSort(int data[], int low, int high)
  /* 用快速排序方法对数组元素data[low..high]作非递减排序 */
  {
    int i, pivotkey, j;
    if(low < high) { /* 以数组的第一个元素为基准（枢轴元素）进行划分 */
      pivotkey = data[low]; i = low; j = high;
      while(i<j) { /* 从数组的两端交替地向中间扫描 */
        while (i<j && data[j]>=pivotkey) j--;
        if (i<j)
          data[i++] = data[j]; /* 比枢轴大元素小者移到低下标端 */
        while(i<j && data[i] <= pivotkey) i++;
        if(i<j)
          data[j--] = data[i]; /* 比枢轴元素大者移到高下标端 */
      }
      data[i] = pivotkey; /* 枢轴元素移到正确的位置 */
      QuickSort(data, low, i-1); /* 对前半个子表递归排序 */
      QuickSort(data, i+1, high); /* 对后半个子表递归排序 */
    }
  }
  ```
- 快速排序是不稳定的排序方法，其平均时间复杂度为 \( O(n \log n) \) ，空间复杂度为 \( O(\log n) \)。若初始记录序列按关键字有序或基本有序时，快速排序则退化为冒泡排序，此时，算法的时间复杂度为O(n^{2})。