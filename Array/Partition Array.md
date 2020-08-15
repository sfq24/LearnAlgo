# Partition Array


### 原题： https://www.lintcode.com/problem/partition-array/description

也可以考虑**双指针**

核心点在于：
1. while终止条件判断
2. 


## 解
用right当做partition，遇到比k小的元素就跟right处的值交换，right进位
```python
class Solution:
    """
    @param nums: The integer array you should partition
    @param k: An integer
    @return: The index after partition
    """
    def partitionArray(self, nums, k):
        # write your code here
        right = 0
        for i in range(0,len(nums)):
            if(nums[i] < k and i >= right):                   # i >= right 是最tricky的部分 一开始i=right的时候也需要进入if让right前进
                temp = nums[right]
                nums[right]=nums[i]
                nums[i] = nums[right]
                right = right + 1
        return right

```

## 解：
双指针，quick sort
```python

```

