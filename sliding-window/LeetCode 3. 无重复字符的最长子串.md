## LeetCode3.无重复字符的最长子串.md
给定一个字符串 s ，请你找出其中不含有重复字符的 最长 子串 的长度。
示例 1:
输入: s = "abcabcbb"
输出: 3 
解释: 因为无重复字符的最长子串是 "abc"，所以其长度为 3。

示例 2:
输入: s = "bbbbb"
输出: 1
解释: 因为无重复字符的最长子串是 "b"，所以其长度为 1。

示例 3:
输入: s = "pwwkew"

输出: 3
解释: 因为无重复字符的最长子串是 "wke"，所以其长度为 3。
     请注意，你的答案必须是 子串 的长度，"pwke" 是一个子序列，不是子串。
 
提示：
0 <= s.length <= 5 * 104
s 由英文字母、数字、符号和空格组成

### 思路
+ 滑动窗口模板题，定义左边界，右边界不断扩大时，判断是否需要收缩左边界。

### 代码
```java
class Solution {
    public int lengthOfLongestSubstring(String s) {
    Map<Character, Integer> lastPos = new HashMap<>();
    int maxLen = 0;
    int left = 0;  // 滑动窗口的左边界

    for (int right = 0; right < s.length(); right++) {
        char c = s.charAt(right);

        // 如果该字符在之前出现过，并且位置 >= 当前窗口左边界
        if (lastPos.containsKey(c) && lastPos.get(c) >= left) {
            // 窗口左边界跳到重复字符的下一位
            left = lastPos.get(c) + 1;
        }

        // 更新字符 c 最新出现的位置
        lastPos.put(c, right);

        // 更新最长子串长度
        maxLen = Math.max(maxLen, right - left + 1);
    }
    return maxLen;
  }

}
```
