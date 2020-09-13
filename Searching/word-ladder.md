# word-ladder

### 原题： https://leetcode.com/problems/word-ladder/

Given two words (beginWord and endWord), and a dictionary's word list, find the length of shortest transformation sequence from beginWord to endWord, such that:

Only one letter can be changed at a time.
Each transformed word must exist in the word list.
Note:

Return 0 if there is no such transformation sequence.
All words have the same length.
All words contain only lowercase alphabetic characters.
You may assume no duplicates in the word list.
You may assume beginWord and endWord are non-empty and are not the same.
Example 1:

Input:
beginWord = "hit",
endWord = "cog",
wordList = ["hot","dot","dog","lot","log","cog"]

Output: 5

Explanation: As one shortest transformation is "hit" -> "hot" -> "dot" -> "dog" -> "cog",
return its length 5.


## 解
BFS
大test case超时。。。。

```c#
public class Solution {
    public int LadderLength(string beginWord, string endWord, IList<string> wordList) {
        if(wordList == null || wordList.Count == 0 || !wordList.Contains(endWord)) return 0;
        
        int length = 0;
        Queue<KeyValuePair<string,List<string>>> queue = new Queue<KeyValuePair<string,List<string>>>();
        
        queue.Enqueue(new KeyValuePair<string,List<string>>(beginWord, new List<string>(wordList)));
        
        while(queue.Count > 0){
            int queueSize = queue.Count;
            length++;
            while(queueSize-- > 0){
                var curr = queue.Dequeue();
                string currWord = curr.Key;
                var currList = curr.Value;
                
                if(currWord == endWord){
                    return length;
                }
                else if(currList.Count == 0){
                    return 0;
                }
                else{
                    foreach(var word in currList){
                        if(DiffOnlyOne(currWord, word)){
                            var newList = new List<string>(currList);
                            newList.Remove(word);
                            queue.Enqueue(new KeyValuePair<string,List<string>>(word, newList));
                        }
                    }
                }
            }
        }
        return 0;
    }
    
    private bool DiffOnlyOne(string word1, string word2){
        
        int diffCount = 0;
        for(int i=0; i < word1.Length; i++){
            if(word1[i] != word2[i]) diffCount++;
            if(diffCount>1) return false;
        }
        
        return diffCount == 1 ? true : false;
    }
}

```


