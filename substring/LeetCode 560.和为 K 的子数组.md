## LeetCode 560.和为 K 的子数组
给你一个整数数组 nums 和一个整数 k ，请你统计并返回 该数组中和为 k 的子数组的个数 。

子数组是数组中元素的连续非空序列。

 

示例 1：

输入：nums = [1,1,1], k = 2
输出：2
示例 2：

输入：nums = [1,2,3], k = 3
输出：2
 

提示：

1 <= nums.length <= 2 * 104
-1000 <= nums[i] <= 1000
-107 <= k <= 107

### 核心思路
+ 前缀和 + 哈希
+ 定义 preSum 表示遍历到当前位置的前缀和；
+ 使用 HashMap 存储 某个前缀和出现的次数；
+ 每到一个位置，判断 (preSum - k) 是否出现过，若出现过说明有以当前位置结尾、和为 k 的子数组；
+ 将当前的 preSum 放入 map 中（累计出现次数）；


### 代码

```java
public int maxArea(int[] height) {
    int left = 0;
    int right = height.length - 1;
    int max = 0;

    while (left < right) {
        // 当前宽度
        int width = right - left;
        // 当前高度为左右中较小的那根柱子
        int h = Math.min(height[left], height[right]);
        // 计算面积并更新最大值
        max = Math.max(max, width * h);

        // 谁矮就移动谁，尝试获得更高的高度
        if (height[left] < height[right]) {
            left++;
        } else {
            right--;
        }
    }

    return max;
}
```
