>[剑指 Offer 11. 旋转数组的最小数字](https://leetcode-cn.com/problems/xuan-zhuan-shu-zu-de-zui-xiao-shu-zi-lcof/)
>
>把一个数组最开始的若干个元素搬到数组的末尾，我们称之为数组的旋转。输入一个递增排序的数组的一个旋转，输出旋转数组的最小元素。例如，数组 [3,4,5,1,2] 为 [1,2,3,4,5] 的一个旋转，该数组的最小值为1。  
>
>**示例1**
```
输入：
  [3,4,5,1,2]
输出：
  1
```
>**示例2**
```
输入：
  [2,2,2,0,1]
输出：
  0
```

```java
// Java版
class Solution {
    public int minArray(int[] numbers) {
        if(numbers.length <= 0){
            return -1;
        }
        int l = 0;
        int r = numbers.length-1;
        // 如果初始状态就是非旋转的状态 那么直接返回最左边
        if(numbers[l] < numbers[r]) {
            return numbers[l];
        }
        while(l < r) {
            int m = l + (r-l)/2;
            // 当前 m 位置为最大值 所以最小值在 m+1 位置
            if(numbers[m] > numbers[m+1]){
                return numbers[m+1];
            }else if(numbers[m] > numbers[l]){
            // 如果中点大于左边 说明最小值可能在 m+1 位置
                l = m+1;
            }else if(numbers[m] < numbers[l]) {
            // 如果中点小于左边 说明最小值可能在 m 的位置（右半边）
                r = m;
            }else if(numbers[m] == numbers[l]) {
            // 如果中点等于左边 有两种可能： 1. 最小值在中点左侧或者右侧 这时只能用左侧坐标去一步一步往右收口
                l++;
                if(numbers[l] < numbers[r]) {
                    return numbers[l];
                }
            }
        }
        return numbers[l];
    }
}
```