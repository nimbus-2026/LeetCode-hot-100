## LeetCode283.移动零
给定一个数组 nums，编写一个函数将所有 0 移动到数组的末尾，同时保持非零元素的相对顺序。

请注意 ，必须在不复制数组的情况下原地对数组进行操作。


示例 1:

输入: nums = [0,1,0,3,12]
输出: [1,3,12,0,0]
示例 2:

输入: nums = [0]
输出: [0]
 

提示:

1 <= nums.length <= 104
-231 <= nums[i] <= 231 - 1
 

进阶：你能尽量减少完成的操作次数吗？

### 思路

使用“快慢指针”，把非 0 元素前移，最后补 0

### 代码
```java
class Solution {
    public void moveZeroes(int[] nums) {
        int slow = 0; // 指向“下一个非零元素应该放的位置”

        // 第一次遍历：把所有非零数挪到数组前面
        for (int i = 0; i < nums.length; i++) {
            if (nums[i] != 0) {
                nums[slow] = nums[i];
                slow++;
            }
        }

        // 第二次遍历：把剩余位置全部填为 0
        while (slow < nums.length) {
            nums[slow] = 0;
            slow++;
        }
    }
}
```
