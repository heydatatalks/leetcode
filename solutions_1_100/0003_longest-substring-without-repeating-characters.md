# 面试便当`python`
解1：双指针实现滑动窗口
#### Python3
```Python
class Solution:
    def lengthOfLongestSubstring(self, s: str) -> int:
        if not s: 
            return 0
        res = 0
        exist = set()
        left, right = -1, 0
        while left < right:
            while right < len(s) and s[right] not in exist:
                exist.add(s[right])
                right += 1
            res = max(right - left - 1, res)
            
            left += 1
            if left < len(s):
                exist.remove(s[left])                
        return res
```
> - 时间复杂度：O(n)
> - 空间复杂度：O(m)，m是 不重复的字符个数
---
# 其他语言版本`Java/Golang/C++`
#### Java
```java
class Solution {
    public int lengthOfLongestSubstring(String s) {
        var exist = new HashSet<Character>();
        int res = 0;
        int left = -1;
        int right = 0;

        while (left < right) {
            while (right < s.length() && !exist.contains(s.charAt(right))) {
                exist.add(s.charAt(right));
                right++;
            }
            res = Math.max(right - left - 1, res);

            left += 1;
            if (left < s.length()) {
                exist.remove(s.charAt(left));
            }
        }
        return res;
    }
}
```
#### Golang
```go
func lengthOfLongestSubstring(s string) int {
    exist := make(map[byte]int8)
    res := 0
    left, right := -1, 0

    for left < right {
        for right < len(s) && exist[s[right]] == 0 {
            exist[s[right]] = 1
            right++
        }
        if right - left - 1 > res {
            res = right - left - 1
        }

        left += 1
        if left < len(s) {
            delete(exist, s[left])
        }
    }

    return res
}
```
#### C++
```cpp
class Solution {
public:
    int lengthOfLongestSubstring(string s) {
        if (s.size() == 0) {
            return 0;
        }
        unordered_set<char> exist;
        int left = -1;
        int right = 0;
        int res = 0;
        while (left < right) {
            while (right < s.size()) {
                auto it = exist.find(s[right]);
                if (it == exist.end()) {
                    exist.insert(s[right]);
                    right++;
                } else {
                    break;
                }
            }
            res = max(right - left - 1, res);

            left++;
            if (left < s.size()) {
                exist.erase(s[left]);
            }
        }
        return res;
    }
};
```