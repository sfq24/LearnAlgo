# Search Insert Position


### 原题： https://www.lintcode.com/problem/search-insert-position/description

Description
Given a sorted array and a target value, return the index if the target is found. If not, return the index where it would be if it were inserted in order.

You may assume NO duplicates in the array.

Have you met this question in a real interview?  
Example
[1,3,5,6], 5 → 2

[1,3,5,6], 2 → 1

[1,3,5,6], 7 → 4

[1,3,5,6], 0 → 0

Challenge
O(log(n)) time



主要区别在于返回值，以及如果target在最前和最后的case

```python
class Solution:
    """
    @param A: an integer sorted array
    @param target: an integer to be inserted
    @return: An integer
    """
    def searchInsert(self, A, target):
        # write your code here
        if(A == None or len(A)==0 or target < A[0]):
            return 0
        if(target > A[-1]):
            return len(A)
        start =0
        end = len(A) -1
        
        while(start + 1 < end):
            mid = int(start + (end - start)/2)
            
            if(A[mid] < target):
                start = mid
            else:
                end = mid
                
        
        if(A[start] == target): 
            return start
        
        return end

```


