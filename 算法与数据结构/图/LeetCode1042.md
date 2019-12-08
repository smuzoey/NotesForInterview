<h1>不邻接植花</h1>

<br>

<h2>题目大意</h2>
N个花园，每个花园你打算种下四种花之一，一个花园最多与三个花园相连，你需要给每个花园选一种花，使得相连两个花园的花不一样。

 [具体题目](https://leetcode-cn.com/problems/flower-planting-with-no-adjacent/) <br>

 **样例1**
> 输入: N = 3, paths = [[1,2], [2,3], [3, 1]]
> 输出: [1, 2, 3]

**样例2**
> 输入: N = 4，paths = [[1,2], [3,4]]
> 输出：[1, 2, 1, 2]

**样例3**
> 输入：N = 4，paths = [[1,2], [2,3], [3,4], [4,1], [1,3], [2, 4]]
> 输出：[1, 2, 3, 4]

<br>
**题目难度：**低
<br>
**题目分类：**图
<br>

<h3>思路</h3>
第一步：将给的path用邻接表存储，mp[x][0] 代表 x 点有几个相连的点，mp[x][1] = y 代表 x 与 y相连， 因为一个点最多与三个点相连，所以我们 mp 数组大小开到5。<br>
第二步：遍历N个点，然后遍历颜色，如果这个颜色和与他相连的都不同，则可以，否则就换颜色 <br>

```Java
class Solution {
    public int[] gardenNoAdj(int N, int[][] paths) {
        // 第一步
        int[][] mp = new int[N + 1][5];
		for(int i = 0; i < paths.length; i++) {
			mp[paths[i][0]][0]++;
			mp[paths[i][1]][0]++;
			mp[paths[i][0]][mp[paths[i][0]][0]] = paths[i][1];
			mp[paths[i][1]][mp[paths[i][1]][0]] = paths[i][0];
		}
		
        // 第二步
		int[] ans = new int[N];
		for(int i = 1; i <= N; i++) { 
			for(int j = 1; j <= 4; j++) {
				boolean flag = false;
				for(int k = 0; k < mp[i][0]; k++) {
					if(ans[mp[i][k+1]-1] == j) {
						flag = true;
					}
				}
				if(flag == false) {
					ans[i-1] = j;
					break;
				}
			}
		}
		return ans;
    }
}
```

