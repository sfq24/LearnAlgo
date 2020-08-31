# Longest Consecutive Sequence

### 原题： https://leetcode.com/problems/longest-consecutive-sequence/

Given an unsorted array of integers, find the length of the longest consecutive elements sequence.

Your algorithm should run in O(n) complexity.

Example:

Input: [100, 4, 200, 1, 3, 2]
Output: 4
Explanation: The longest consecutive elements sequence is [1, 2, 3, 4]. Therefore its length is 4.


第一遍用HashTable存元素，再排序 ====》 直接用SortedSet
用另一个int存consecutive长度

```c# 
public class Solution {
    public int LongestConsecutive(int[] nums) {
        if(nums == null || nums.Length == 0) return 0;
        SortedSet<int> hashset = new SortedSet<int>();
        int res = 1;
        
        foreach(int num in nums){
            if(!hashset.Contains(num)) hashset.Add(num);
        }
        
        int consec = 1;
        
        //hashset.OrderBy(s => s);
        
        foreach(int num in hashset){
            //Console.WriteLine(num);
            if(hashset.Contains(num-1)){
                consec++;
                res = Math.Max(res, consec);
            }
            else{
                consec = 1;
            }
        }
        
        return res;
    }
}
```


