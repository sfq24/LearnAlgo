# Two Sum


### 原题： https://leetcode.com/problems/two-sum

最粗暴依然考虑**双指针**，达到O（n2）

核心点在于：
1. 注意c# 表达数组的语法 


## 解1
time 》 60%
mem 》 97%
```c#
public class Solution {
    public int[] TwoSum(int[] nums, int target) {
        int[] result = {0,1};        //注意初始化方法
        if(nums.Length <=2){
            return result;
        }
        for(int pre = 0; pre < nums.Length -1; pre++){
            for(int post = pre +1; post < nums.Length; post++){
                if(nums[post] == target - nums[pre]){
                    result[0] = pre;
                    result[1] = post;
                    return result;
                }
            }
        }
        return result;
    }
}

```

### 另解 (更优） Hashtable：
待补充

```c#


```
