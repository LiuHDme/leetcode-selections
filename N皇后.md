**代码描述**

n 皇后问题研究的是如何将 n 个皇后放置在 n×n 的棋盘上，并且使皇后彼此之间不能相互攻击。

![img](http://liuhdme-blog.oss-cn-beijing.aliyuncs.com/2020-10-30-080712.png)

上图为 8 皇后问题的一种解法。

给定一个整数 n，返回所有不同的 n 皇后问题的解决方案。

每一种解法包含一个明确的 n 皇后问题的棋子放置方案，该方案中 'Q' 和 '.' 分别代表了皇后和空位。

示例：

```
输入：4
输出：[
 [".Q..",  // 解法 1
  "...Q",
  "Q...",
  "..Q."],

 ["..Q.",  // 解法 2
  "Q...",
  "...Q",
  ".Q.."]
]
解释: 4 皇后问题存在两个不同的解法。
```

**提示：**

- 皇后彼此不能相互攻击，也就是说：任何两个皇后都不能处于同一条横行、纵行或斜线上。

**代码**

```python
class Solution:
    def solveNQueens(self, n: int) -> List[List[str]]:
        ans = []
        cols, pie, na = [], [], []
        self.dfs(n, ans, cols, pie, na, 1)
        return ans

    def dfs(self, n, ans, cols, pie, na, row):
        if row == n + 1:
            self.draw(ans, cols)
            return
        for col in range(1, n + 1):
            if col in cols or (row + col) in pie or (n - row + 1 + col) in na:
                continue
            cols.append(col)
            pie.append(col + row)
            na.append(n - row + 1 + col)
            self.dfs(n, ans, cols, pie, na, row + 1)
            cols.pop()
            pie.pop()
            na.pop()

    def draw(self, ans, cols):
        pic = []
        for row in range(1, len(cols) + 1):
            temp = ['.'] * len(cols)
            temp[cols[row - 1] - 1] = 'Q'
            temp = ''.join(temp)
            pic.append(temp)
        ans.append(pic)
```

