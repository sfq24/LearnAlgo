## 切片操作
~~~python3
def rotate(self, nums: List[int], k: int) -> None:
    k = k % len(nums)        # k 可能大于数组长度
    nums.reverse()           # 整体翻转
    nums[:k] = nums[:k][::-1]   # 前 k 个翻转
    nums[k:] = nums[k:][::-1]   # 后面翻转
~~~



## Map操作
~~~python3
def maxWealth(self, accounts: List[List[int]]) -> int:
    return max(map(sum, accounts))
# map，第一个是用的函数，第二个是可迭代的对象
~~~
