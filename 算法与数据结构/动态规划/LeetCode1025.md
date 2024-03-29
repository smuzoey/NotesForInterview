
## 01 Leetcode 1025除数博弈

难度：简单

[具体题目请点击](https://leetcode-cn.com/problems/divisor-game/)

**题目大意:**

A B 两人玩游戏 , 轮流进行, A 先手, A 胜利则输出 true, A失败输出 false

游戏内容:

给一个数字n, 你可以进行一次操作,  将 n 变为 n-x, 

n的要求: x必须满足 n % x == 0(n可以被x整除) 并且  0 < x < n

 

**分析:**

1:  false   A先手 没有数字被1整除还小于1的 所以A不能进行操作, A输

2: true   A将2变为1, B不能进行操作, A胜利

3: false  A将3变为2, B将2变为1, A面对1, 无法操作, A输

.....

n --->  n - x   

如果 n-x 是true, 那么n 会false;   比如 3 ---> 2

如果 n-x 是false, 那么 n 会true; 比如 2 ---> 1 

 

我们可以将全部的1~n的胜负都用循环跑出来

bool divisorGame(int N){
    int a[1010];  //0代表false, 1代表true
    for(int i = 0; i <= N; i++) a[i] = 0;  //默认全部为0
    a[1] = 0, a[2] = 1, a[3] = 0;

    for(int i = 4; i <= N; i++) {    
        for(int j = 1; j < i; j++) {
            if(i % j == 0 && a[i-j] == 0) {   //一旦有一个数可以让i赢, 那么i就一定会赢, 最优的策略   
                a[i] = 1;
                break;
            }
        }
    }

    if(a[N] == 0) return false;       
    else return true;
}

 

看到一个dp题就要开始先推推样例, 你在推的过程中就可能会发现 奇数先手输, 偶数先手赢这个规律

为什么呢?

1: false

2: true

3: false

4: true

5: false

6: 我们将6-1   1的胜负是false, 按照我们说的规则, n-x=5 是false 则会 true    则6是true   

7: 满足7的 x 只能为1  则 n-x = 6为 true, 则7为false

 

偶数减去1 一定为奇数, 奇数一定会输, 那么偶数就会赢   //我们要赢, 所以就让一个偶数减去奇数就好

奇数减去1 一定是偶数, 偶数会赢, 那么奇数就会输....减去1奇数会输, 我们能不能减去偶数呢?       

答案是不能:  因为奇数不可能和一个偶数 被整除, 所以奇数一定减去的是奇数

 

所以如果按照博弈来做的话, 还可以直接判断奇数和偶数



我这拙劣的文笔!
 

 
