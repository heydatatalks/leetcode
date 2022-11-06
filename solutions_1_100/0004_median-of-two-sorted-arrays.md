# 面试便当`python`

解：当两数组总长度和为偶数时，在数组A和数组B中，
1. 在A、B分别寻找一个分割i和j，得到A<sub>左</sub>与A<sub>右</sub>，B<sub>左</sub>与B<sub>右</sub>
2. 保持count(A<sub>左</sub> + B<sub>左</sub>) == count(A<sub>右</sub> + B<sub>右</sub>)
3. 二分查找i，使得max(A<sub>左</sub> + B<sub>左</sub>) < min(A<sub>右</sub> + B<sub>右</sub>)，得解。

奇数同理。
#### Python3
```Python
class Solution:
    def findMedianSortedArrays(self, nums1: List[int], nums2: List[int]) -> float:
        m, n = len(nums1), len(nums2)
        if m > n:
            return self.findMedianSortedArrays(nums2, nums1)

        left, right = 0, m
        left_max, right_min = 0, 0
        M_MIN_INT = -1 * 10e8
        M_MAX_INT = 10e8

        while left <= right:
            i = (left + right) // 2
            j = (m + n + 1) // 2 - i

            nums_i_m1 = M_MIN_INT if i == 0 else nums1[i - 1]
            nums_i = M_MAX_INT if i == m else nums1[i]
            nums_j_m1 = M_MIN_INT if j == 0 else nums2[j - 1]
            nums_j = M_MAX_INT if j == n else nums2[j]

            left_max = max(nums_i_m1, nums_j_m1)
            right_min = min(nums_i, nums_j)
            if left_max <= right_min:
                # 找到了正确分割，停止查找
                break
            else:
                # 若分割有误，则仅有如下两种情况
                if nums_i_m1 > nums_j:
                    right = i - 1
                elif nums_j_m1 > nums_i:
                    left = i + 1

        return (left_max + right_min) / 2.0 if (m + n) % 2 == 0 else left_max
```
> - 时间复杂度：O(log(min(m, n)))
> - 空间复杂度：O(1)
---
# 其他语言版本`Java/Golang/C++`
#### Java
```Java
class Solution {
    public double findMedianSortedArrays(int[] nums1, int[] nums2) {
        int m = nums1.length;
        int n = nums2.length;
        if (m > n) {
            return findMedianSortedArrays(nums2, nums1);
        }

        
        int left = 0;
        int right = m;
        int leftMax = 0;
        int rightMin = 0;

        while (left <= right) {
            int i = (left + right) / 2;
            int j = (m + n + 1) / 2 - i;

            int numsIm1 = (i == 0 ? Integer.MIN_VALUE : nums1[i - 1]);
            int numsI = (i == m ? Integer.MAX_VALUE : nums1[i]);
            int numsJm1 = (j == 0 ? Integer.MIN_VALUE : nums2[j - 1]);
            int numsJ = (j == n ? Integer.MAX_VALUE : nums2[j]);

            leftMax = Math.max(numsIm1, numsJm1);
            rightMin = Math.min(numsI, numsJ);
            if (leftMax <= rightMin) {
                // 找到了正确分割，停止查找
                break;
            } else {
                // 若分割有误，则仅有如下两种情况
                if (numsIm1 > numsJ) {
                    right = i - 1;
                } else if (numsJm1 > numsI) {
                    left = i + 1;
                }
            }
        }

        return (m + n) % 2 == 0 ? (leftMax + rightMin) / 2.0 : leftMax;
    }
}
```
#### Golang
```go
func findMedianSortedArrays(nums1 []int, nums2 []int) float64 {
    m, n := len(nums1), len(nums2)
    if n < m {
        return findMedianSortedArrays(nums2, nums1)
    }

    left, right := 0, m
    leftMax, rightMin := 0, 0
    const M_INT_MIN = int(-1 * 10e5)
    const M_INT_MAX = int(10e5)

    for left <= right {
        i := (left + right) / 2
        j := (m + n + 1) / 2 - i

        numsIm1 := M_INT_MIN
        if i > 0 { numsIm1 = nums1[i - 1]}
        numsI := M_INT_MAX
        if i < m { numsI = nums1[i]}
        numsJm1 := M_INT_MIN
        if j > 0 { numsJm1 = nums2[j - 1]}
        numsJ := M_INT_MAX
        if j < n { numsJ = nums2[j]}

        leftMax = getMax(numsIm1, numsJm1)
        rightMin = getMin(numsI, numsJ)
        if leftMax <= rightMin {
            // 找到了正确分割，停止查找
            break
        } else {
            // 若分割有误，则仅有如下两种情况
            if numsIm1 > numsJ {
                right = i - 1;
            } else if numsJm1 > numsI {
                left = i + 1;
            }
        }
    }

    res := 0.0
    if (m + n) % 2 == 0 {
        res = float64(leftMax + rightMin) / 2.0
    } else {
        res = float64(leftMax)
    }
    return res
}

func getMax(a int, b int) int {
    if a > b { return a }
    return b
}

func getMin(a int, b int) int {
    if a > b { return b }
    return a
}
```
#### C++
```cpp
class Solution {
public:
    double findMedianSortedArrays(vector<int>& nums1, vector<int>& nums2) {
        int m = nums1.size();
        int n = nums2.size();
        if (n < m) {
            return findMedianSortedArrays(nums2, nums1);
        }

        int left = 0, right = m;
        int leftMax = 0, rightMin = 0;

        while (left <= right) {
            int i = (left + right) / 2;
            int j = (m + n + 1) / 2 - i;

            int nums1Im1 = (i == 0 ? INT32_MIN : nums1[i - 1]);
            int nums1I = (i == m ? INT32_MAX : nums1[i]);
            int nums2Jm1 = (j == 0 ? INT32_MIN : nums2[j - 1]);
            int nums2J = (j == n ? INT32_MAX : nums2[j]);

            leftMax = max(nums1Im1, nums2Jm1);
            rightMin = min(nums1I, nums2J);

            if (leftMax <= rightMin) {
                break;
            } else {
                if (nums1Im1 > nums2J) {
                    right = i - 1;
                } else if (nums2Jm1 > nums1I) {
                    left = i + 1;
                }
            }
        }
        return (m + n) % 2 == 0 ? (leftMax + rightMin) / 2.0 : leftMax;
    }
};
```