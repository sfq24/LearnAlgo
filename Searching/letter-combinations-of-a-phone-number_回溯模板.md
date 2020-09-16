# letter-combinations-of-a-phone-number

### 原题： https://leetcode.com/problems/letter-combinations-of-a-phone-number/

Given a string containing digits from 2-9 inclusive, return all possible letter combinations that the number could represent.

A mapping of digit to letters (just like on the telephone buttons) is given below. Note that 1 does not map to any letters.



Example:

Input: "23"
Output: ["ad", "ae", "af", "bd", "be", "bf", "cd", "ce", "cf"].


backtracing典型题
**注意初始化dictionary**
**注意如何向string加减元素**

# 解 回溯

```c#
public class Solution {
    public IList<string> LetterCombinations(string digits) {
        List<string> res = new List<string>();
        
        if(digits == null || digits.Length == 0) return res;
        
        Dictionary<char, string> map = new Dictionary<char, string> {{'2',"abc"}, {'3',"def"}, {'4',"ghi"}, {'5',"jkl"}, {'6',"mno"}, {'7',"pqrs"}, {'8',"tuv"}, {'9',"wxyz"}};
    
        DFS(digits, 0, "", map, res);
        
        return res;
    }
    
    private void DFS(string digits, int index, string comb, Dictionary<char, string> map, List<string> res){
        if(comb.Length == digits.Length){      //判断终止条件
            res.Add(new string(comb));
            return;
        }

        
        for(int i = index; i < digits.Length; i++){
            foreach(var letter in map[digits[i]]){
                comb += letter;                      
                DFS(digits, i + 1, comb, map, res);            //进位递归
       
                comb = comb.Remove(comb.Length -1);            //剪枝
            }

        }

    }
}
```


# 解 循环

```c#
public class Solution {
    public IList<string> LetterCombinations(string digits) {
        List<string> result = new List<string>();
        if(digits == null || digits.Length == 0){
            return result;
        }
        Dictionary<char, char[]> map = new Dictionary<char, char[]>();
        map.Add('1', new char[] {});
        map.Add('2', new char[]{'a','b','c'});
        map.Add('3', new char[]{'d','e','f'});
        map.Add('4', new char[]{'g','h','i'});
        map.Add('5', new char[]{'j','k','l'});
        map.Add('6', new char[]{'m','n','o'});
        map.Add('7', new char[]{'p','q','r','s'});
        map.Add('8', new char[]{'t','u','v'});
        map.Add('9', new char[]{'w','x','y','z'});

        result.Add("");
        List<string> temp = new List<string>();
        foreach (var digit in digits){
            temp.Clear();
            foreach(var str in result){
                foreach(var letter in map[digit]){
                    temp.Add(str+letter);
                }
            }
            result = new List<string>(temp);
        }
        return result;
        
    }
}

```


