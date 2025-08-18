## LeetCode 438. 找到字符串中所有字母异位词.md
给定两个字符串 s 和 p，找到 s 中所有 p 的 异位词 的子串，返回这些子串的起始索引。不考虑答案输出的顺序。

示例 1:

输入: s = "cbaebabacd", p = "abc"
输出: [0,6]
解释:
起始索引等于 0 的子串是 "cba", 它是 "abc" 的异位词。
起始索引等于 6 的子串是 "bac", 它是 "abc" 的异位词。

示例 2:

输入: s = "abab", p = "ab"
输出: [0,1,2]
解释:
起始索引等于 0 的子串是 "ab", 它是 "ab" 的异位词。
起始索引等于 1 的子串是 "ba", 它是 "ab" 的异位词。
起始索引等于 2 的子串是 "ab", 它是 "ab" 的异位词。
 

提示:
1 <= s.length, p.length <= 3 * 104
s 和 p 仅包含小写字母


### 思路

我这里写的是滑动窗口的题解，固定窗口也可以。

可以把它分成三个阶段：

1. 扩张窗口
  + right++
  + 更新窗口 map
  + 如果该字符满足次数要求，valid++

2. 窗口判断
  + 当 right - left >= p.length()
  + 如果 valid == need.size() → 窗口是异位词 → add
  + 收缩左边界

3. left++
  + 更新窗口 map
  + 如果移出字符导致数量不满足 → valid--

### 代码

```java
public List<Integer> findAnagrams(String s, String p) {
    List<Integer> res = new ArrayList<>();
    if (s.length() < p.length()) {
        return res;
    }

    Map<Character, Integer> need = new HashMap<>();
    Map<Character, Integer> window = new HashMap<>();

    for (char ch : p.toCharArray()) {
        need.put(ch, need.getOrDefault(ch, 0) + 1);
    }

    int left = 0, right = 0;
    int valid = 0;

    while (right < s.length()) {
        char cur = s.charAt(right);
        right++;

        if (need.containsKey(cur)) {
            window.put(cur, window.getOrDefault(cur, 0) + 1);
            if (window.get(cur).equals(need.get(cur))) {
                valid++;
            }
        }

        // 当窗口大小 >= p.length() 时收缩左边界
        while (right - left >= p.length()) {
            char leftChar = s.charAt(left);

            if (valid == need.size()) {
                // 当前窗口已经是 p 的一个排列，因此窗口中的字符（包括 leftChar）一定都属于 p
                res.add(left);
            }

            left++;
            if (need.containsKey(leftChar)) {
                int count = window.get(leftChar) - 1;
                window.put(leftChar, count);
                if (count < need.get(leftChar)) {
                    valid--;
                }
            }
        }
    }
    return res;
}

```
