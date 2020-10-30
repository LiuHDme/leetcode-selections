**题目描述**

https://leetcode-cn.com/problems/combination-sum-iv/

给定一个由正整数组成且不存在重复数字的数组，找出和为给定目标正整数的组合的个数。

示例:

```
nums = [1, 2, 3]
target = 4

所有可能的组合为：
(1, 1, 1, 1)
(1, 1, 2)
(1, 2, 1)
(1, 3)
(2, 1, 1)
(2, 2)
(3, 1)

请注意，顺序不同的序列被视作不同的组合。

因此输出为 7。
```

**代码**

1. 回溯（超时）

   ```java
   class Solution {
       // 回溯，超时
       public int combinationSum4(int[] nums, int target) {
           List<List<Integer>> ans = new ArrayList<>();
           Deque<Integer> stack = new LinkedList<>();
           dfs(nums, target, ans, stack);
           return ans.size();
       }
   
       private void dfs(int[] nums, int target, List<List<Integer>> ans, Deque<Integer> stack) {
           if (target == 0) {
               ans.add(new ArrayList(stack));
               return;
           }
   
           for (int i = 0; i < nums.length; i++) {
               if (nums[i] > target) continue;
               stack.add(nums[i]);
               dfs(nums, target - nums[i], ans, stack);
               stack.pollLast();
           }
       }
   }
   ```

2. dp

   ```java
   class Solution {
       public int combinationSum4(int[] nums, int target) {
           int[] dp = new int[target + 1];
           dp[0] = 1;
   
           for (int i = 1; i <= target; i++) {
               for (int num : nums) {
                   if (num <= i)
                       dp[i] += dp[i - num];
               }
           }
   
           return dp[target];
       }
   }
   ```

**Note** 这种只求结果个数用dp