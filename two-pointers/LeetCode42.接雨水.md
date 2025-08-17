## LeetCode42. 接雨水
给定 n 个非负整数表示每个宽度为 1 的柱子的高度图，计算按此排列的柱子，下雨之后能接多少雨水。

 <img width="412" height="161" alt="image" src="https://github.com/user-attachments/assets/5f0dbe22-1a35-44ab-9e63-43372f8d1f60" />


输入：height = [0,1,0,2,1,0,1,3,2,1,2,1]
输出：6
解释：上面是由数组 [0,1,0,2,1,0,1,3,2,1,2,1] 表示的高度图，在这种情况下，可以接 6 个单位的雨水（蓝色部分表示雨水）。

示例 2：

输入：height = [4,2,0,3,2,5]
输出：9
 

提示：

n == height.length
1 <= n <= 2 * 104
0 <= height[i] <= 105

### 思路

+ 当前位置能接多少水 = 左右最高高度的较小值 − 当前高度
+ 有点小技巧

### 代码
```java
class Solution {
    public int trap(int[] height) {
    int left = 0, right = height.length - 1;
    int leftMax = 0, rightMax = 0;
    int res = 0;

    // 双指针向中间靠拢
    while (left < right) {
        if (height[left] < height[right]) {
            // 更新左边的最大高度
            leftMax = Math.max(leftMax, height[left]);
            // leftMax - 当前高度 = 此处可接的水量
            res += (leftMax - height[left]);
            left++;
        } else {
            // 更新右边的最大高度
            rightMax = Math.max(rightMax, height[right]);
            // rightMax - 当前高度 = 此处可接的水量
            res += (rightMax - height[right]);
            right--;
        }
    }
    return res;
  }

}
```
