# 面试便当`python`
#### Python3
解1：排序+双指针
```Python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        aux = [(nums[i], i) for i in range(len(nums))]
        aux.sort()
        left, right = 0, len(nums) - 1
        while left < right:
            if aux[left][0] + aux[right][0] == target:
                return [aux[left][1], aux[right][1]]
            elif aux[left][0] + aux[right][0] < target:
                left += 1
            else:
                right -= 1
        return None
```
> - 时间复杂度：O(nlogn)，排序nlogn，搜索n，合并复杂度nlogn
> - 空间复杂度：O(n)，因为申请了和nums等长的辅助数组

解2：哈希表O(1)查找
~~~
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        exist = {}
        for i, num in enumerate(nums):
            if target - num in exist:
                return [exist[target - num], i]
            exist[nums[i]] = i
        return []
~~~
> - 时间复杂度：O(n)，一层简单循环
> - 空间复杂度：O(n)，申请了和nums同量级的dict
---
# 其他语言版本`Java/Golang/C++`
#### Java
~~~
class Solution {
    public int[] twoSum(int[] nums, int target) {
        HashMap<Integer, Integer> exist = new HashMap();
        for (int i = 0; i < nums.length; i++) {
            if (exist.containsKey(target - nums[i])) {
                return new int[]{i, exist.get(target - nums[i])};
            }
            exist.put(nums[i], i);
        }
        return null;
    }
}
~~~

#### Golang
~~~
func twoSum(nums []int, target int) []int {
    exist := make(map[int]int)
    for i, v := range nums {
        if index, ok := exist[target - v]; ok {
            return []int{index, i}
        }
        exist[v] = i
    }
    return nil
}
~~~

#### C++
~~~
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        unordered_map<int, int> exist;
        for (size_t i = 0; i < nums.size(); ++i) {
            auto it = exist.find(target - nums[i]);
            if ( it != exist.end()) {
                return {it->second, (int)i};
            }
            exist[nums[i]] = i;
        }
        return {};
    }
};
~~~

