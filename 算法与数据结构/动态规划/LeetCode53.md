# 最大子序列和

## 题目大意：
给一个数组，求出最大子序列和（连续数的和最大）

**例子**
> 输入: [-2,1,-3,4,-1,2,1,-5,4],
> 输出: 6
> 解释: 连续子数组 [4,-1,2,1] 的和最大，为 6。

<br>
<br>

## 1、动态规划
如果按动态规划的做法，我们已知的条件：
1. 前 n-1 个数最大的子序列和 ans
2. num[n] 的值

<br>

我们还差一个条件：包括**num[n-1]的连续值**的最大值 sum

样例中前缀和（sum）的值

前缀和小于0则默认为0，最后面的值不会有任何帮助

| 0| 0 |0 |4 |-3|5 |6 |1  |5 |
| :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | 
 
<br>
最终 ans = max(ans, sum + num[i]);

代码
```
复杂度：O(n)

class Solution {
    public int maxSubArray(int[] nums) {
        int len = nums.length;
        int sum = 0;  // 前缀和
        int ans = nums[0];  //最大值
        for(int i = 0; i < len; i++) {
            ans = Math.max(ans, sum + nums[i]);
            sum = sum + nums[i];
            if(sum < 0) sum = 0; 
        }
        return ans;
    }
}
```

<br>
<br>


