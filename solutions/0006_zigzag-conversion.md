# 面试便当`python`
解1：
#### Python3
```Python
class Solution:
    def convert(self, s: str, numRows: int) -> str:
        if numRows == 1:
            return s
        buffer = [[] for _ in range(numRows)]

        inc = 1
        cur = 0
        for i, v in enumerate(s):
            buffer[cur].append(v)
            cur += inc
            if cur < 0 or cur >= numRows:
                inc *= -1
                cur += inc * 2

        res = ""
        for i in range(numRows):
            res += "".join(buffer[i])
        return res
```
> - 时间复杂度：O(n)
> - 空间复杂度：O(n)，看上去是二维list，其实总长和numRows一致
---
# 其他语言版本`Java/Golang/C++`
#### Java
```Java
class Solution {
    public String convert(String s, int numRows) {
        if (numRows == 1) {
            return s;
        }

        var buffer = new ArrayList<StringBuffer>();
        for (int i = 0; i < numRows; ++i) { 
            buffer.add(new StringBuffer());
        }

        int inc = 1;
        int cur = 0;
        for (int i = 0; i < s.length(); ++i) {
            buffer.get(cur).append(s.charAt(i));
            cur += inc;
            if (cur < 0 || cur >= numRows) {
                inc *= -1;
                cur += inc * 2;
            }
        }

        var ans = new StringBuffer();
        for (StringBuffer sb : buffer) {
            ans.append(sb);
        }

        return ans.toString();
    }
}
```
#### Golang
```go
func convert(s string, numRows int) string {
    if numRows == 1 {
        return s
    }

    a := make([]string, numRows)
    inc := 1
    cur := 0

    for _, v := range s {
        a[cur] += string(v)
        cur += inc
        if cur < 0 || cur >= numRows {
            inc *= -1
            cur += inc * 2
        }
    }

    return strings.Join(a, "")
}  
```
#### C++
```cpp
class Solution {
public:
    string convert(string s, int numRows) {
        if (numRows == 1) {
            return s;
        }

        string a[numRows];
        int inc = 1;
        int cur = 0;

        for (size_t i = 0; i < s.size(); ++i) {
            a[cur] += s[i];
            cur += inc;
            if (cur < 0 || cur >= numRows) {
                inc *= -1; 
                cur += inc * 2;
            }
        }

        string res;
        for (auto& sub : a) {
            res += sub;
        }
        return res;
    }
};
```