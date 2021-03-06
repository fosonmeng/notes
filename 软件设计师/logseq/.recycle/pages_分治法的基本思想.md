- 分治与递归就像一对孪生兄弟，经常同时应用于算法设计之中，并由此产生许多高效的算法。我们知道，任何一个可以用计算机求解的问题所需要的计算时间都与其规模有关。问题的规模越小，解题所需要的计算时间往往也越少，从而也较容易处理。例如，对于n个元素的排序问题，当n=1时，不需任何比较；当n=2时，只要做一次比较即可；…而当n较大时，问题就不那么容易处理了。要想直接解决一个较大的问题，有时是相当困难的。分治法的设计思想是将一个难以直接解决的大问题分解成一些规模较小的相同问题以便各个击破，分而治之。如果规模为n的问题可分解成k个子问题，1<k<=n，这些子问题互相独立且与原问题相同。分治法产生的子问题往往是原问题的较小模式，这就为递归技术提供了方便。
- 一般来说，分治算法在每一层递归上都有三个步骤。
  1. 分解。将原问题分解成一系列子问题。
  2. 求解。递归地求解各子问题。若子问题足够小，则直接求解。
  3. 合并。将子问题的解合并成原问题的解。
-