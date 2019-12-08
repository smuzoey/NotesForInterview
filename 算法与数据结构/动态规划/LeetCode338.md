<h1>比特位计数</h1>
<br>
<h2>题目大意</h2>
给一个数num，返回一个数组，数组是0~num的二进制有多少个1

[具体题目](https://leetcode-cn.com/problems/counting-bits/)
<br>

**样例**
> 输入：5
> 输出：[0,1,1,2,1,2]
<br>

**题目难度：** 简单

**题目类型：** LeetCode分类是动态规划，不过其实就是一个普通思维题，不过也用到记忆化吧。。

<br>

<h2>思路</h2>
其实最暴力的就是 nlgn 的复杂度，每一个数都去除2，能除多少次2就是多少个1，然后复杂度为 n 的做法也很简单，如果你了解二进制的化，×2 相当于在后面加一个0，并未添加1，所以如果 x % 2 == 0 则 x 的1的个数等于 x/2 的；如果不能被2整除呢？则说明x比 [x-1] 的1的个数多 1。

<br>
<br>

```Java
class Solution {
    public int[] countBits(int num) {
        int[] ans = new int[num + 1];
        ans[0] = 0;
        for(int i = 1; i <= num; i++) {
            if(i % 2 == 0) {
                ans[i] = ans[i/2];
            } else {
                ans[i] = ans[i-1] + 1;
            }
        }
        return ans;
    }
}
```