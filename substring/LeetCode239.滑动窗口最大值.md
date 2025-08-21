## LeetCode11.盛最多水的容器
给你一个整数数组 nums，有一个大小为 k 的滑动窗口从数组的最左侧移动到数组的最右侧。你只可以看到在滑动窗口内的 k 个数字。滑动窗口每次只向右移动一位。

返回 滑动窗口中的最大值 。

 

示例 1：

输入：nums = [1,3,-1,-3,5,3,6,7], k = 3
输出：[3,3,5,5,6,7]
解释：
滑动窗口的位置                最大值
---------------               -----
[1  3  -1] -3  5  3  6  7       3
 1 [3  -1  -3] 5  3  6  7       3
 1  3 [-1  -3  5] 3  6  7       5
 1  3  -1 [-3  5  3] 6  7       5
 1  3  -1  -3 [5  3  6] 7       6
 1  3  -1  -3  5 [3  6  7]      7

示例 2：

输入：nums = [1], k = 1
输出：[1]
 

提示：

1 <= nums.length <= 105
-104 <= nums[i] <= 104
1 <= k <= nums.length

### 核心思路
+ 维护一个“从大到小”的单调栈，队首就是窗口最大值


### 代码

```java
public int[] maxSlidingWindow(int[] nums, int k) {
    if (nums == null || nums.length == 0) return new int[0];

    int n = nums.length;
    int[] res = new int[n - k + 1];
    // 双端队列：存储的是数组元素的“索引”
    Deque<Integer> deque = new ArrayDeque<>();

    for (int i = 0; i < n; i++) {
        // 1. 移除队尾中所有比当前元素小的值（它们永远不可能成为最大值了）
        while (!deque.isEmpty() && nums[deque.peekLast()] < nums[i]) {
            deque.pollLast();
        }

        // 2. 当前索引加入队尾
        deque.offerLast(i);

        // 3. 如果队首元素已经不在当前窗口范围，则移除
        if (deque.peekFirst() <= i - k) {
            deque.pollFirst();
        }

        // 4. 当窗口长度达到 k 时，记录窗口最大值（即队首的值）
        if (i >= k - 1) {
            res[i - k + 1] = nums[deque.peekFirst()];
        }
    }
    return res;
}
```
