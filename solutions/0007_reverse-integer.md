# 面试便当`python`
解1：有两个坑，一是不能对MIN_INT取绝对值，二是中间环节不能使用到int64
#### Python3
```Python
class Solution:
    def reverse(self, x: int) -> int:
        MAX_INT = 2**30 - 1 + 2**30
        MIN_INT = MAX_INT * (-1) - 1
        if x == MIN_INT :
            return 0

        res = 0
        sign = 1 if x >= 0 else -1
        x = abs(x)

        while x != 0:
            val = x % 10
            if sign > 0:
                if res > MAX_INT // 10 or (res == MAX_INT // 10 and val > MAX_INT % 10):
                    return 0
            if sign < 0:
                if res > MAX_INT // 10 or (res == MAX_INT // 10 and val > MAX_INT % 10 + 1):
                    return 0
            x = x // 10
            res = res * 10 + val
        return res * sign

```
> - 时间复杂度：O(n)，n为x的十进制位数
> - 空间复杂度：O(1)
---
# 其他语言版本`Java/Golang/C++`
#### Java
```Java
class Solution {
    public int reverse(int x) {
        if (x == Integer.MIN_VALUE) {return 0;}

        int res = 0;
        int sign = x > 0 ? 1 : -1;
        x = Math.abs(x);

        while (x > 0) {
            int val = x % 10;
            if (sign > 0) {
                if (res > Integer.MAX_VALUE / 10 || 
                (res == Integer.MAX_VALUE / 10 && val >= Integer.MAX_VALUE % 10)) {
                    return 0;
                }
            } else {
                if (res > Integer.MAX_VALUE / 10 || 
                (res == Integer.MAX_VALUE / 10 && val >= Integer.MAX_VALUE % 10 + 1)) {
                    return 0;
                }
            }
            x = x / 10;
            res = res * 10 + val;
        }
        return res * sign;
    }
}
```
#### Golang
```go
func reverse(x int) int {
    INT_MAX := (1 << 30) - 1 + (1 << 30)
    INT_MIN := INT_MAX * (-1) - 1
    if x == INT_MIN {
        return 0
    }

    res, sign := 0, 1
    if x < 0 {
        sign = -1
        x = -1 * x
    }
    
    for x > 0 {
        val := x % 10
        if sign > 0 {
            if res > INT_MAX / 10 || (res == INT_MAX / 10 && val > INT_MAX % 10) {
                return 0
            }
        } else {
            if res > INT_MAX / 10 || (res == INT_MAX / 10 && val > INT_MAX % 10 + 1) {
                return 0
            }
        }
        x = x / 10
        res = res * 10 + val
    }

    return res * sign
}
```
#### C++
```cpp
class Solution {
public:
    int reverse(int x) {
        if (x == INT_MIN) { return 0;}
        
        int res = 0;
        int sign = 1;
        if (x < 0) {
            sign = -1;
            x = -1 * x;
        }
        while (x > 0) {
            int val = x % 10;
            if (sign > 0) {
                if (res > INT_MAX / 10 || (res == INT_MAX / 10 && val > INT_MAX % 10)) {
                    return 0;
                }
            } else {
                if (res > INT_MAX / 10 || (res == INT_MAX / 10 && val > INT_MAX % 10 + 1)) {
                    return 0;
                }
            }
            x = x / 10;
            res = res * 10 + val;
        }
        return res * sign;
    }
};
```