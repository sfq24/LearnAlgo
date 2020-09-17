# restore-ip-addresses

### 原题： https://leetcode.com/problems/restore-ip-addresses/

Given a string s containing only digits, return all possible valid IP addresses that can be obtained from s. You can return them in any order.

A valid IP address consists of exactly four integers, each integer is between 0 and 255, separated by single dots and cannot have leading zeros. For example, "0.1.2.201" and "192.168.1.1" are valid IP addresses and "0.011.255.245", "192.168.1.312" and "192.168@1.1" are invalid IP addresses. 

Example 1:

Input: s = "25525511135"
Output: ["255.255.11.135","255.255.111.35"]
Example 2:

Input: s = "0000"
Output: ["0.0.0.0"]
Example 3:

Input: s = "1111"
Output: ["1.1.1.1"]
Example 4:

Input: s = "010010"
Output: ["0.10.0.10","0.100.1.0"]
Example 5:

Input: s = "101023"
Output: ["1.0.10.23","1.0.102.3","10.1.0.23","10.10.2.3","101.0.2.3"]
 

Constraints:

0 <= s.length <= 3000
s consists of digits only.


回溯法做

# 解
这题需要好好研究，好几个index，考虑好怎样迭代。
好几个边界条件： 开头为0的情况，s太长太短情况等

注意几个语法：
Int16.Parse（string）

str = str.Substring(pos) :     from pos to end
str = str.Substring(start, len):     from start, length

str = str.Remove(pos) :        from pos to end
str = str.Remove(start, end):  from start to end      

```c#
public class Solution {
    public IList<string> RestoreIpAddresses(string s) {
        List<string> res = new List<string>();
        if(s == null || s.Length<4 || s.Length > 16) return res;
        
        Helper(0, s, "", res);
        
        return res;
        
    }
    
    //k 为四个ip域循环
    private void Helper(int k, string s, string ipAddr, List<string> res){
        
        if(k == 4 || s.Length == 0){
            if(k == 4 && s.Length ==0){
                res.Add(new string(ipAddr));        //照相法
            }
            return;
        }
        
        //i为三个数字循环
        for(int i=0; i<s.Length && i <=2; i++){
            if(i != 0 && s[0] == '0'){          //注意此处判断！！！！
                break;
            }
            string part = s.Substring(0, i + 1);
            //Console.WriteLine(part);
            
            if(Int16.Parse(part) <= 255){
                if(k > 0){
                    part = '.' + part;
                }

                ipAddr += part;

                Helper(k + 1, s.Substring(i+1), ipAddr, res);
                ipAddr = ipAddr.Remove(ipAddr.Length - part.Length);
            }

        }
    }
    
}

```


