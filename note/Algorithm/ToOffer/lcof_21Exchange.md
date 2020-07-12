>[剑指 Offer 21. 调整数组顺序使奇数位于偶数前面](https://leetcode-cn.com/problems/diao-zheng-shu-zu-shun-xu-shi-qi-shu-wei-yu-ou-shu-qian-mian-lcof/)
>
>输入一个整数数组，实现一个函数来调整该数组中数字的顺序，使得所有奇数位于数组的前半部分，所有偶数位于数组的后半部分。
>
>**示例1**
```
输入：
  nums = [1,2,3,4]
输出：
  [1,3,2,4]
```

```golang
// Golang版
// 保持了奇数和偶数的相对顺序 - 相对较慢
func exchange(nums []int) {
    if len(nums) <= 0 {
        return
    }
    // 表示下一个奇数 应该存在的位置
    j := 0
    for i := 0; i < len(nums); i++ {
        // 如果当前数值为奇数
        if nums[i]%2 == 1 {
            // 如果当前奇数的位置 大于 应该存在的位置，那就说明混入了偶数，需要后移元素
            if i > j {
                k := i
                tmp := nums[i]
                for k > j {
                    // 元素后移
                    nums[k] = nums[k-1]
                    k--
                }
                // 赋值
                nums[k] = tmp
            }
            // 更新下一个奇数的位置
            j++
        }
    }
}
```
```golang
// 无需保持顺序 - 符合题意
func exchange(nums []int) {
    if len(nums) <= 0 {
        return
    }
    i, j := 0, len(nums)-1
    for i < j {
        for i < j && nums[i]%2 == 1 {
            i++
        }
        for i < j && nums[j]%2 == 0 {
            j--
        }
        nums[i], nums[j] = nums[j], nums[i]
    }
}
```