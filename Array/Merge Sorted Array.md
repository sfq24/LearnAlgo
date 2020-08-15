# Merge Sorted Array

### 原题： https://leetcode.com/problems/merge-sorted-array/

倒着考虑，从选出最大的从尾部往里放。 最后只需考虑剩下的nums2剩余情况。如果nums1剩余，说明不需要其他操作，已经是sorted。

核心点在于：
1. while终止条件判断
2. 数组加指针的简洁用法


## 解
```c#
public class Solution {
    public void Merge(int[] nums1, int m, int[] nums2, int n) {

        int i = m - 1;
        int j = n - 1;
        int end = m + n -1;

        while(i >= 0 && j >= 0){
            if(nums1[i] > nums2[j]){
                nums1[end--] = nums1[i--];
            }
            else{
                nums1[end--] = nums2[j--];
            }
        }
        
        while(j >= 0){
            nums1[end--] = nums2[j--];
        }
    }
}

```

