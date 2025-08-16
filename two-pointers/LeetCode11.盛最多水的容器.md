## LeetCode11.盛最多水的容器
给定一个长度为 n 的整数数组 height 。有 n 条垂线，第 i 条线的两个端点是 (i, 0) 和 (i, height[i]) 。

找出其中的两条线，使得它们与 x 轴共同构成的容器可以容纳最多的水。

返回容器可以储存的最大水量。

说明：你不能倾斜容器。

示例 1：
输入：[1,8,6,2,5,4,8,3,7]
输出：49 
解释：图中垂直线代表输入数组 [1,8,6,2,5,4,8,3,7]。在此情况下，容器能够容纳水（表示为蓝色部分）的最大值为 49。

示例 2：
输入：height = [1,1]
输出：1

提示：

n == height.length
2 <= n <= 105
0 <= height[i] <= 104

### 核心思路
面积 = 宽 × 高，而高度取决于较短的一根柱子。
使用双指针，从两端开始遍历。
这样做有一个好处：控制变量法，宽度在不断变小。

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
