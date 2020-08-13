# Subarray Sum


### 原题： https://www.lintcode.com/problem/subarray-sum

因为题目要求返回任一个和为0的subarray即可。 而且必然有和为0的subarray
依然考虑**双指针**，达到O（n2）。
注意考虑几个corner case：[0], [1,0,1], [-3,3]等

核心点在于：
1. corner case 判断：
2. 终止条件


## 解1
》 60%
```python
class Solution:
    """
    @param nums: A list of integers
    @return: A list of integers includes the index of the first number and the index of the last number
    """
    def subarraySum(self, nums):
        # write your code here
        if nums == None or len(nums)==1:     #corner case 判断
            return[0,0]

        for pre in range(0,len(nums)-1):        #不能让sum=nums[pre], 然后post从pre+1开始循环,否则[1,0,1] fail
            sum = 0
            for post in range(pre, len(nums)):
                sum += nums[post]
                if sum == 0:
                    return [pre, post]

```

### 另解 (更优） Hashtable：
待补充

```c#


```
