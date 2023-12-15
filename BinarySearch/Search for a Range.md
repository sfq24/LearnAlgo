#  Search for a Range

### 原题： https://www.lintcode.com/problem/search-for-a-range/

Given a sorted array of n integers, find the starting and ending position of a given target value.

If the target is not found in the array, return [-1, -1].

Have you met this question in a real interview?  
Example
Example 1:

Input:
[]
9
Output:
[-1,-1]

Example 2:

Input:
[5, 7, 7, 8, 8, 10]
8
Output:
[3, 4]

## 其实是O（n）：
直接2分法，最后前后找boundary，注意几个corner case： [], [1] 1


```python
class Solution:
    """
    @param A: an integer sorted array
    @param target: an integer to be inserted
    @return: a list of length 2, [index1, index2]
    """
    def searchRange(self, A, target):
        # write your code here
        if(A == None or len(A) == 0):
            return [-1,-1]
        start = 0
        end = len(A) - 1
        
        while(start + 1 < end):
            mid = int(start + (end - start)/2)
            if(A[mid] < target):
                start = mid
            else:
                end = mid
                
        
        if(A[start] != target and A[end] != target):
            return [-1, -1]
            
        start = end
        
        while(start >= 0 and A[start] == target):
            start -= 1
            
        while(end < len(A) and A[end] == target):
            end += 1
            
        return [start+1, end-1]
    
            

        

```


## 真正O(logn):

```java
public int[] searchRange(int[] a, int target) {
        // write your code here
        if (a == null || a.length == 0) {
            return new int[] {-1, -1};
        }

        int start = 0, end = a.length - 1;
        int left = -1;

        // find left boundary
        while (start + 1 < end) {
            int mid = start + (end - start) / 2;

            if (a[mid] >= target) {
                end = mid;
            } else {
                start = mid;
            }
        }

        if (a[start] == target) {
            left = start;
        } else if (a[end] == target) {
            left = end;
        } else {
            return new int[] {-1, -1};
        }

        start = 0;
        end = a.length - 1;
        int right = -1;
        // find right boundary
        while (start + 1 < end) {
            int mid = start + (end - start) / 2;

            if (a[mid] <= target) {
                start = mid;
            } else {
                end = mid;
            }
        }

        if (a[end] == target) {
            right = end;
        } else if (a[start] == target) {
            right = start;
        } else {
            return new int[] {-1, -1};
        }

        return new int[] {left, right};
    }

```
