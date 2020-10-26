**题目描述**

实现 [pow(*x*, *n*)](https://www.cplusplus.com/reference/valarray/pow/) ，即计算 x 的 n 次幂函数。

示例 1:

```
输入: 2.00000, 10
输出: 1024.00000
```

示例 2:

```
输入: 2.10000, 3
输出: 9.26100
```

示例 3:

```
输入: 2.00000, -2
输出: 0.25000
解释: 2-2 = 1/22 = 1/4 = 0.25
```

说明:

- -100.0 < x < 100.0
- n 是 32 位有符号整数，其数值范围是 [$−2^{31}$,  $2^{31} − 1$] 。

**代码**

```java
class Solution {
    public double myPow(double x, int n) {
        long N = n;
        if (n < 0) {
            N = -N;
            x = 1 / x;
        }
        return calculate(x, N);
    }

    private double calculate(double x, long N) {
        if (N < 1) return 1;

        double half = calculate(x, N / 2);

        return N % 2 == 0 ? half * half : half * half * x;
    }
}
```



