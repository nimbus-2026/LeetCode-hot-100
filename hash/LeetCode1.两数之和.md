## LeetCode 1. 两数之和
给定一个整数数组 nums 和一个整数目标值 target，请你在该数组中找出 和为目标值 target  的那 两个 整数，并返回它们的数组下标。

你可以假设每种输入只会对应一个答案，并且你不能使用两次相同的元素。

你可以按任意顺序返回答案。

示例 1：
输入：nums = [2,7,11,15], target = 9
输出：[0,1]
解释：因为 nums[0] + nums[1] == 9 ，返回 [0, 1] 。

示例 2：
输入：nums = [3,2,4], target = 6
输出：[1,2]

示例 3：
输入：nums = [3,3], target = 6
输出：[0,1]
 

**提示：**
2 <= nums.length <= 104
-109 <= nums[i] <= 109
-109 <= target <= 109
只会存在一个有效答案

### 思路

用一个 HashMap 保存 值 → 索引

遍历数组，当前值为 num，目标补数为 target - num

如果补数已存在于 map 中，说明找到了答案

否则把当前元素放入 map，继续遍历

### 代码
```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
    // key：数值  value：索引
    Map<Integer, Integer> map = new HashMap<>();
    for (int i = 0; i < nums.length; i++) {
        int need = target - nums[i];
        // 如果补数已经出现过，直接返回结果
        if (map.containsKey(need)) {
            return new int[]{map.get(need), i};
        }
        // 否则把当前数放进 map，供后面使用
        map.put(nums[i], i);
    }
    return new int[]{-1, -1};
  }
}
```
