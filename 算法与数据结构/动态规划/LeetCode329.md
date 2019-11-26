## LeetCode 329.判断子序列

<br>
题意: 给s, t两个字符串, 判断s是否是t的字符串<br>
例如:  s = "abc",   t = "ahbgdc"<br>   
输出: true<br>

[具体题目请点击](https://leetcode-cn.com/problems/is-subsequence/)
<br>


<h2> 方法一:  直接判断 </h2>

 复杂度 O(n)
 
 
```
        int slen = s.size();
        int tlen = t.size();

        if(slen > tlen) {
            return false;
        }

        int i = 0, j = 0;
        while(i < tlen) {
            if(t[i] == s[j]) i++, j++;
            else i++;
        }

        if(j >= slen) return true;
        else return false;
```
考虑一下为什么i与j有时均更新, 有时只更新i
<br>
<br>

<h2>方法二: 动态规划 </h2>

复杂度 O(nm)

动态规划思想:
<font color=#8B3626>将待解决问题分成若干个子问题, 先解决子问题, 然后再从子问题得到原问题;这个时候容易想到分治法, 但是与分治法不同的是,  动态规划分解的子问题往往是有联系的.动态规划的基本思路是保存已解决的子问题的答案, 不管该子问题以后是否被用到, 只要它被计算过, 就将其填入表中  </font>
<br>

**构建表**

这道题怎样去构建表呢?  
我们构建一个二维布尔表   **dp[len(s)][len(t)]**

<font color=#8B3626>dp[i][j]  = true  代表:  s字符串前i个字符是t字符串前j个字符的子串</font>
我们这道题的答案是什么呢?    dp[len(s)][len(t)] 为true代表s是t的子串,为false,代表s不是t的字串
<br>
**初始化表dp[i][j]**
用题目中的例子   s = "abc" ,   t = "ahbgdc"

dp表的初始化为如下:

  | true  |  true  |  true  |  true  |  true   |  true  |  true   |
  | :---:    |  :---: |  :---:  |  :---:  |  :---:   |  :---:  |  :---:   |
  | false  |             |      |    |     |    |    | 
  | false  |             |   |    |     |    |   | 
  | false  |             |    |    |     |    |   |  
<br>

<font color=#8B3626>空字符串是任何字符串的子串</font>
dp[0][0]=true, &ensp; "" 是否是 "" 的子串 
dp[0][1]=true, &ensp; "" 是否是 "a" 的子串
dp[0][2]=true, &ensp;  "" 是否是 "ah" 的字串
...
dp[0][len(t)]=true 代表: "" 是 "ahbgdc" 的子串
<br>
<font color=#8B3626>除了空字符串, 任何字符串都不会是空字符串的子串</font>
dp[1][0]=false, &ensp; "a" 不是 ""  的子串
dp[2][0]=false, &ensp; "ab" 不是 "" 的子串
dp[3][0]=false, &ensp; "abc" 不是 "" 的子串
...

<br>

**更新表**
s = "abc" ,   t = "ahbgdc"  

通过判断 s[i] == t[j] 更新 dp[i][j] 
**dp[1][1]代表:**  s[1] = 'a', t[1] = 'a',    s[1] == t[1]   dp[1][1] = true (代表"a" 是 "a" 的子串)
**dp[1][2]代表:**  s[1] = 'a', t[2] = 'h',    s[1]  != t[2]   dp[1][2]  = ?  
等于false?   "a" 是 "ah" 的子串
等于ture?    "a" != "h"  怎样得 true 呢?
<br>
此时需要<font color=red>状态转移方程式</font> , 根据dp[i][j] 前面的去更新dp[i][j]  
```
if(s[i] == t[j]) 
    dp[i][j] = dp[i-1][j-1];
else if(s[i] != t[j])
    dp[i][j] = dp[i][j-1];

```


建议将表格填一遍: 
更新一行  

  | true  |  true  |  true  |  true  |  true   |  true  |  true   |
  | :---:    |  :---: |  :---:  |  :---:  |  :---:   |  :---:  |  :---:   |
  | false  | true        |true  |true|true |true|true| 
  | false  |             |   |    |     |    |   | 
  | false  |             |    |    |     |    |   |  

第二行 dp[1][1~6] 均为true 代表  "a"  是  "a"; "ah", "ahb", "ahbg", "ahbgd", "ahbgdc" 的子串
<br>

再更新一行

  | true  |  true  |  true  |  true  |  true   |  true  |  true   |
  | :---:    |  :---: |  :---:  |  :---:  |  :---:   |  :---:  |  :---:   |
  | false  | true        |true  |true|true |true|true| 
  | false  |     false   |false |true|true|  true| true  | 
  | false  |             |    |    |     |    |   |  

第三行
s = "abc" ,   t = "ahbgdc"    
s[2] != t[1]  "ab" 是 "a" 的子串?   false
s[2] != t[2] "ab" 是 "ah"的子串?  false
s[2] == t[3] && dp[1][2]  "a"是"ah"的子串,  所以 "ab" 是 "ahb" 的子串?  true 
.....
<br>
```
        int sLen = s.length(), tLen = t.length();
        if (sLen > tLen) return false;
        if (sLen == 0) return true;
        boolean[][] dp = new boolean[sLen + 1][tLen + 1];
  
        for (int j = 0; j < tLen; j++) {
            dp[0][j] = true;
        }
    
        for (int i = 1; i <= sLen; i++) {
            for (int j = 1; j <= tLen; j++) {
                if (s.charAt(i - 1) == t.charAt(j - 1)) {
                    dp[i][j] = dp[i - 1][j - 1];
                } else {
                    dp[i][j] = dp[i][j - 1];
                }
            }
        }
        return dp[sLen][tLen];
```
<br>
总结:
1. dp[i][j] : 代表 s的前i个字符  是否是  t前j个字符的子串
2. 在判断dp[i][j] 的时候,  dp[0~i-1][0~j-1]的结果我们已经知道
3. 所以这道题就是我们知道 三个条件   
      1. dp[lens-1][lent-1] = true    "ab"是"ahbgd"的子串
      2. dp[lens-1][lent]  = false   "ab"不是"ahbgdc"的子串
      3. dp[lens][lent-1] = false    "abc"不是"ahbgd"的子串
   根据这三个条件去判断dp[lens][lent]  , 这也就是转移方程

<br>

<h2>扩展: 最长公共子序列 </h2>

给两个字符串s, t,  求出这两个字符串最长的公共子序列的长度
例如:  s = "abcd",   t = "becd"    
输出: 3("bcd")

这个例子初始化表格
![avatar](https://images.cnblogs.com/cnblogs_com/smuzoey/1600093/o_1911260246421.png)

完整表格
![avatar](https://images.cnblogs.com/cnblogs_com/smuzoey/1600093/o_1911260246552.png)


转移方程式为
```
if(s[i] == t[j])
     dp[i][j] = max(dp[i-1][j], dp[i][j-1], dp[i-1][j-1]+ 1);
else if(s[i] != t[j])
     dp[i][j] = max(dp[i-1][j], dp[i][j+1]);
```


