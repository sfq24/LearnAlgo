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


## Dictionary操作
~~~python3
def is_anagram(s: str, t: str) -> bool:
    if len(s) != len(t):
        return False

    count = {}
    for ch in s:
        count[ch] = count.get(ch, 0) + 1
    for ch in t:
        count[ch] = count.get(ch, 0) - 1

    return all(v == 0 for v in count.values())


for k in d:               # 遍历 key
for k in d.keys():        # 同上，显式写法
for v in d.values():      # 遍历 value
for k, v in d.items():    # 遍历键值对 ← 最常用

# 带 index
for i, (k, v) in enumerate(d.items()):


# 按 key 排序
sorted(d.items())                        # [(k,v), ...] key 升序
sorted(d.items(), reverse=True)          # key 降序

# 按 value 排序 ← 高频考点
sorted(d.items(), key=lambda x: x[1])          # value 升序
sorted(d.items(), key=lambda x: -x[1])         # value 降序
sorted(d.items(), key=lambda x: x[1], reverse=True)

~~~


## 字符转数字
~~~python3
def is_anagram(s: str, t: str) -> bool:
    if len(s) != len(t):
        return False

    count = [0] * 26
    for ch in s:
        count[ord(ch) - ord('a')] += 1
    for ch in t:
        count[ord(ch) - ord('a')] -= 1

    return all(c == 0 for c in count)
~~~

