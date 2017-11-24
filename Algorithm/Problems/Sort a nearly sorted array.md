（facebook 面经)

# Sort a nearly sorted (or K sorted) array

(http://www.geeksforgeeks.org/medium/)

Given an array of n elements, where each element is at most k away from its target position, devise an algorithm that sorts in O(n log k) time. 
For example, let us consider k is 2, an element at index 7 in the sorted array, can be at indexes 5, 6, 7, 8, 9 in the given array.

看到这题就想起了 Youssef 的其中考试，那是3sorted array，前面还有一道小题是提示先计算此位置之前的最大元素，例如数组[1,1,2,1,1,1,2,3,1,4,5]，“此位置（包含此位置）之前的最大元素”可以用[1,1,2,2,2,2,2,3,3,4,5]来表示，以下称这个数组为“最大元素数组”，可以看出来它是一个非递减数组。

我当时的做法是：

从数组后面来看，最后一个**最大元素数组元素**肯定就是数组中的最大元素，所以如果数组中的最后一个元素和最大元素相等，那么说明这个位置时正确的，继续看前一位，4也是在正确的位置，再来看前一位，数组元素是1，最大元素是3，说明这个位置应该是3而不是1，由于我们要找的3距离这个1一定不超过3，所以在数组中距离1不超过3的位置之中找一个3，和这个3替换位置，由于后面的数组已经是排好了的，所以只在前3个里面找就可以了，那么就在前面的三个元素1，2，3里面找到3，我们把3挪过来，数组变成了[1,1,2,1,1,1,2,**1,3**,4,5]，此时要更新最大元素数组，但我们可以不从头更新，因为只有挪动的两个元素之间（区间[)左闭右开）的最大数组元素可能发生改变，对应挪动的两个元素1，3本来的最大数组元素是3，3，现在变成了2，3。更新最大数组元素和构造它的方法一样，看本位置的元素是不是比上一个位置的最大数组元素大，如果大的话本位置的最大元素数组元素和本位置元素相等，否则和上一位最大元素数组相等。更新完之后最大数组变成了[1,1,2,2,2,2,2,2,3,4,5]此时检查了三个位置，后三个位置已经排好，然后继续往前看，数组中钱一个元素时1（是我们刚交换位置的那个），但是最大数组中的元素是2，找到2并且换了位置以后数组变成了[1,1,2,1,1,1,**1,2**,3,4,5]，然后更新最大数组，以此类推。

如果前面的3个元素有多个我们要找的元素，替换第一个就行了，例如[2,2,2,1]最大数组是[2,2,2,2]，我们把1和第一个2替换似乎更符合直觉，因为如果和最后一个2换，以后肯定还要和前面的2来换

类似的，如果时 k sorted，我们还是利用最大元素数组，每次在前 k 个元素之中找替换就可以了