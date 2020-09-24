# House Robber

### 原题： https://leetcode.com/problems/house-robber/

You are a professional robber planning to rob houses along a street. Each house has a certain amount of money stashed, the only constraint stopping you from robbing each of them is that adjacent houses have security system connected and it will automatically contact the police if two adjacent houses were broken into on the same night.

Given a list of non-negative integers representing the amount of money of each house, determine the maximum amount of money you can rob tonight without alerting the police.

 

Example 1:

Input: nums = [1,2,3,1]
Output: 4
Explanation: Rob house 1 (money = 1) and then rob house 3 (money = 3).
             Total amount you can rob = 1 + 3 = 4.
Example 2:

Input: nums = [2,7,9,3,1]
Output: 12
Explanation: Rob house 1 (money = 2), rob house 3 (money = 9) and rob house 5 (money = 1).
             Total amount you can rob = 2 + 9 + 1 = 12.


可进一步状态压缩

```c#
public class Solution {
    public int Rob(int[] nums) {
        if(nums.Length == 0) return 0;
        if(nums.Length == 1) return nums[0];
        
        int[] money = new int[nums.Length];
        
        money[0] = nums[0];
        money[1] = nums[0] > nums[1] ? nums[0] : nums[1];         //注意此处初始化
        
        for(int i = 2; i< nums.Length; i++){
            money[i] = Math.Max(nums[i] + money[i - 2], money[i-1]);
        }
        
        return money[nums.Length - 1];
    }

}

```


循环房： arranged in a circle
其实仔细考虑，就是两种情况比较0---n-2打劫， 和1---n-1打劫。  （不循环是0---n-2）打劫。
特殊情况是会有一种情况两头都没打劫，只打劫了（1---n-2），这时候另外一种情况肯定会cover住或头或尾的case


```c#
public class Solution {
    public int Rob(int[] nums) {
        if(nums == null || nums.Length == 0) return 0;
        if(nums.Length < 2) return nums[0];
        
        return Math.Max(Helper(nums, 0, nums.Length-1), Helper(nums, 1, nums.Length));
    }
    
    private int Helper(int[] nums, int start, int last){
        int pre = 0, post = 0;
        int curr = 0;
        for(int i = start; i < last; i++){
            curr = Math.Max(post, pre + nums[i]);
            pre = post;
            post = curr;
        }
        return curr;
    }
}

```