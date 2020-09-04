# first-bad-version


### 原题： https://www.lintcode.com/problem/first-bad-version

代码库的版本号是从 1 到 n 的整数。某一天，有人提交了错误版本的代码，因此造成自身及之后版本的代码在单元测试中均出错。请找出第一个错误的版本号。

你可以通过 isBadVersion 的接口来判断版本号 version 是否在单元测试中出错，具体接口详情和调用方法请见代码的注释部分。

请阅读代码编辑框内注释代码，获取对于不同语言正确调用 isBadVersion 的方法，比如java的调用方式是SVNRepo.isBadVersion(v)

样例
n = 5:

    isBadVersion(3) -> false
    isBadVersion(5) -> true
    isBadVersion(4) -> true

因此可以确定第四个版本是第一个错误版本。
挑战
调用 isBadVersion 的次数越少越好


## 解
直接2分

```python
#class SVNRepo:
#    @classmethod
#    def isBadVersion(cls, id)
#        # Run unit tests to check whether verison `id` is a bad version
#        # return true if unit tests passed else false.
# You can use SVNRepo.isBadVersion(10) to check whether version 10 is a 
# bad version.
class Solution:
    """
    @param n: An integer
    @return: An integer which is the first bad version.
    """
    def findFirstBadVersion(self, n):
        # write your code here
        if(n == 1):
            return 1
        
        start = 1
        end = n
        
        while(start + 1 < end):
            mid = int(start + (end - start)/2)
            if(SVNRepo.isBadVersion(mid) == False):
                start = mid
            else:
                end = mid
                
        
        if(SVNRepo.isBadVersion(start) == True):
            return start
        
        return end

```


