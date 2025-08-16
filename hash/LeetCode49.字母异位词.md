## LeetCode49.字母异位词
给你一个字符串数组，请你将 字母异位词 组合在一起。可以按任意顺序返回结果列表。

 

示例 1:

输入: strs = ["eat", "tea", "tan", "ate", "nat", "bat"]

输出: [["bat"],["nat","tan"],["ate","eat","tea"]]

解释：

在 strs 中没有字符串可以通过重新排列来形成 "bat"。
字符串 "nat" 和 "tan" 是字母异位词，因为它们可以重新排列以形成彼此。
字符串 "ate" ，"eat" 和 "tea" 是字母异位词，因为它们可以重新排列以形成彼此。
示例 2:

输入: strs = [""]

输出: [[""]]

示例 3:

输入: strs = ["a"]

输出: [["a"]]

 

提示：

1 <= strs.length <= 104
0 <= strs[i].length <= 100
strs[i] 仅包含小写字母

### 思路

使用 Map<String, List<String>> 保存 key → 排序/计数后的字符串，value → 原字符串列表

遍历每个字符串，将其字母排序（或计数），作为 key

将原字符串加入对应 key 的列表

遍历结束后返回所有 value 组成的列表

### 代码
```java
class Solution {
    public List<List<String>> groupAnagrams(String[] strs) {
        // key: 排序后的字符串  value: 原字符串列表
        Map<String, List<String>> map = new HashMap<>();
        for (String s : strs) {
            // 将字符串字符排序，得到唯一 key
            char[] chars = s.toCharArray();
            Arrays.sort(chars);
            String key = new String(chars);

            // 如果 key 不存在，先创建新列表
            if (!map.containsKey(key)) {
                map.put(key, new ArrayList<>());
            }
            // 加入当前字符串
            map.get(key).add(s);
        }
        // 返回所有分组结果
        return new ArrayList<>(map.values());
    }
}
```
