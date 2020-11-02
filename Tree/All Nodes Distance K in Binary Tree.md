# All Nodes Distance K in Binary Tree

### 原题： https://leetcode-cn.com/problems/all-nodes-distance-k-in-binary-tree/

We are given a binary tree (with root node root), a target node, and an integer value K.

Return a list of the values of all nodes that have a distance K from the target node.  The answer can be returned in any order.

 
## 解 DFS
核心思路，递归找。分别向left，right 和 parent方向找k-1 distance的node

所以：1. 需要用dictionary 存 每个node对应的parent （DFS）
     2. 每个访问过的node标记为visited，不然来回move也被算distance
     3. DFS找 depth

```c#
public class Solution {
    public IList<int> DistanceK(TreeNode root, TreeNode target, int K) {
        Dictionary<TreeNode, TreeNode> parDict = new Dictionary<TreeNode, TreeNode>();
        List<int> res = new List<int>();
        HashSet<TreeNode> visited = new HashSet<TreeNode>();

        MapParents(root, null, parDict);      //form parent dict

        FindKthNode(target, K, res, parDict, visited);  //从target开始DFS

        return res;

    }

  //多加了parent node让DFS更简便， 也可以只传node本身，再分别处理left， right
    void MapParents(TreeNode node, TreeNode par, Dictionary<TreeNode, TreeNode> parDict){           
        if(node != null){
            parDict.Add(node, par);
            MapParents(node.left, node, parDict);
            MapParents(node.right, node, parDict);
        }
    }

    void FindKthNode(TreeNode node, int K, List<int> res, Dictionary<TreeNode, TreeNode> parDict, HashSet<TreeNode> visited){
        if(visited.Contains(node)) return;
        
        visited.Add(node);

        if(K == 0){
            res.Add(node.val);
            return;
        }
        
        
        //3 个方向找
        if(node.left != null){
            FindKthNode(node.left, K - 1, res, parDict, visited);
        }
        if(node.right != null){
            FindKthNode(node.right, K - 1, res, parDict, visited);
        }
        if(parDict[node] != null){
            FindKthNode(parDict[node], K - 1, res, parDict, visited);
        }
    }
}
```


## 解
BFS

用null在queue中做每一层的分隔。每次遇到null就知道到了新的layer，进行判断

```java
class Solution {
    Map<TreeNode, TreeNode> parent;
    public List<Integer> distanceK(TreeNode root, TreeNode target, int K) {
        parent = new HashMap();
        dfs(root, null);

        Queue<TreeNode> queue = new LinkedList();
        queue.add(null);
        queue.add(target);

        Set<TreeNode> seen = new HashSet();
        seen.add(target);
        seen.add(null);

        int dist = 0;
        while (!queue.isEmpty()) {
            TreeNode node = queue.poll();
            if (node == null) {
                if (dist == K) {
                    List<Integer> ans = new ArrayList();
                    for (TreeNode n: queue)
                        ans.add(n.val);
                    return ans;
                }
                queue.offer(null);
                dist++;
            } else {
                if (!seen.contains(node.left)) {
                    seen.add(node.left);
                    queue.offer(node.left);
                }
                if (!seen.contains(node.right)) {
                    seen.add(node.right);
                    queue.offer(node.right);
                }
                TreeNode par = parent.get(node);
                if (!seen.contains(par)) {
                    seen.add(par);
                    queue.offer(par);
                }
            }
        }

        return new ArrayList<Integer>();
    }

    public void dfs(TreeNode node, TreeNode par) {
        if (node != null) {
            parent.put(node, par);
            dfs(node.left, node);
            dfs(node.right, node);
        }
    }
}

```
