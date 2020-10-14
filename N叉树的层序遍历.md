给定一个 N 叉树，返回其节点值的*层序遍历*。 (即从左到右，逐层遍历)。

例如，给定一个 `3叉树` :

<img src="https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2018/10/12/narytreeexample.png" style="zoom:50%;" />

返回其层序遍历:

```
[
     [1],
     [3,2,4],
     [5,6]
]
```

1. 迭代（队列）

   ```java
   class Solution {
       public List<List<Integer>> levelOrder(Node root) {
           if (root == null) return new ArrayList<List<Integer>> ();
           List<List<Integer>> ans = new ArrayList<> ();
           Deque<Node> queue = new LinkedList<Node> ();
           queue.addFirst(root);
           while (!queue.isEmpty()) {
               int size = queue.size();
               List<Integer> tmp = new ArrayList<> ();
               for (int i = 0; i < size; i++) {
                   Node node = queue.pollFirst();
                   queue.addAll(node.children);
                   tmp.add(node.val);
               }
               ans.add(tmp);
           }
           return ans;
       }
   }
   ```

2. 递归

   ```java
   class Solution {
       public List<List<Integer>> levelOrder(Node root) {
           List<List<Integer>> ans = new ArrayList<> ();
           helper(root, ans, 0);
           return ans;
       }
   
       public void helper(Node root, List<List<Integer>> ans, int level) {
           if (root == null) return;
           
           if (ans.size() <= level) ans.add(new ArrayList<Integer> ());
           ans.get(level).add(root.val);
           
           for (Node child : root.children)
               helper(child, ans, level + 1);
       }
   }
   ```

   

