# 面试便当`python`
解1：中心扩散，应付面试应该是没问题的
#### Python3
```Python
class Solution:
    def longestPalindrome(self, s: str) -> str:
        if not s:
            return ""
        res = s[0]

        for i in range(len(s)):
            # 单中心节点情况
            left, right = i, i
            while left >= 0 and right < len(s) and s[left] == s[right]:
                left -= 1
                right += 1
            res = res if right - left - 1 < len(res) else s[left+1:right]
            
            # 双中心节点情况
            if i + 1 < len(s) and s[i] == s[i + 1]:
                left, right = i, i + 1
                while left >= 0 and right < len(s) and s[left] == s[right]:
                    left -= 1
                    right += 1
                res = res if right - left - 1 < len(res) else s[left+1:right]

        return res
```
> - 时间复杂度：O(n<sup>2</sup>)
> - 空间复杂度：O(1)
---
# 其他语言版本`Java/Golang/C++`
#### Java
```Java
class Solution {
    public String longestPalindrome(String s) {
        if (s == null || s.length() == 0) {
            return "";
        }
        String res = s.substring(0, 1);

        for (int i = 0; i < s.length(); i++) {
            // single node as pivot
            int left = i, right = i;
            while (left >= 0 && right < s.length() && s.charAt(left)==s.charAt(right)) {
                left--;
                right++;
            }
            res = right - left - 1 > res.length() ? s.substring(left+1, right) : res;

            // double nodes as pivot
            if (i + 1 < s.length() && s.charAt(i) == s.charAt(i + 1)) {
                left = i;
                right = i + 1;
                while (left >= 0 && right < s.length() && s.charAt(left)==s.charAt(right)) {
                    left--;
                    right++;
                }
                res = right - left - 1 > res.length() ? s.substring(left+1, right) : res;
            }
        }
        return res;
    }
}
```
#### Golang
```go
func longestPalindrome(s string) string {
    if len(s) == 0 {
        return ""
    }
    res := s[0:1]

    for i, _ := range s {
        // single node as pivot
        left, right := i, i
        for left >= 0 && right < len(s) && s[left] == s[right] {
            left--
            right++
        }
        if right - left - 1 > len(res) {
            res = s[left + 1:right]
        }

        if i + 1 < len(s) && s[i] == s[i + 1] {
            left, right = i, i + 1
            // double nodes as pivot
            for left >= 0 && right < len(s) && s[left] == s[right] {
                left--
                right++
            }
            if right - left - 1 > len(res) {
                res = s[left + 1:right]
            }
        }
        
    }
    return res
}
```
#### C++
```cpp
class Solution {
public:
    string longestPalindrome(string s) {
        if (s.size() == 0) {
            return "";
        }

        string res(1, s[0]);

        for (int i = 0; i < s.size(); ++i) {
            // single node as pivot
            int left = i, right = i;
            while (left >= 0 && right < s.size() && s[left] == s[right]) {
                --left;
                ++right;
            }
            res = right - left - 1 > res.size() ? s.substr(left + 1, right - left - 1) : res;

            if (i + 1 < s.size() && s[i] == s[i + 1]) {
                // double nodes as pivot
                left = i;
                right = i + 1;
                while (left >= 0 && right < s.size() && s[left] == s[right]) {
                    --left;
                    ++right;
                }
                res = right - left - 1 > res.size() ? s.substr(left + 1, right - left - 1) : res;
            }
        }

        return res;
    }
};
```