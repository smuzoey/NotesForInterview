<h1>全排列</h1>
<br>
<h2>题目大意</h2>
给定一个没有重复数字的序列，返回其所有可能的全排列

[题目链接](https://leetcode-cn.com/problems/permutations/)
<br>

**样例**
> 输入: [1,2,3]
> 输出:
> [
>  [1,2,3],
>  [1,3,2],
>  [2,1,3],
>  [2,3,1],
>  [3,1,2],
>  [3,2,1]
>]

<br>

**题目难度：** 中等
**题目分类：** dfs
<br>

<h2>思路一</h2>
分析全排列发现其实全排列就是每个数字所在的位置都变化一次，下面的代码进行变换，固定x以及x之前的数，然后变换后面的。如果看不懂下面的dfs，建议按代码手推一遍。
<br>

```Java
class Solution {
  public void solve(List<List<Integer>> ans,ArrayList<Integer> list, int x) {

    	int len = list.size();
		if(x == len) {
			ans.add(new ArrayList<Integer>(list));
		}
		for(int i = x; i < len; i++) {
			Collections.swap(list, x, i);
			solve(ans, list, x + 1);
			Collections.swap(list, x, i);
		}
  }

  public List<List<Integer>> permute(int[] nums) {

		List<List<Integer>> ans = new LinkedList();
		ArrayList<Integer> numList = new ArrayList<Integer>();
		for(int num : nums) {
			numList.add(num);
		}
		solve(ans, numList, 0);
		return ans;
  }
}

```

<br>
<br>
<h2>思路2</h2>
dfs, 思路1是交换，思路2就是添加，flag[i] = 1 代表 num[i] 在当前列表中。<br>

```JAVA
class Solution {
	public List<List<Integer>> permute(int[] nums) {
		List<List<Integer>> ans = new ArrayList<>();
		List<Integer> tmp = new ArrayList<>();
		int[] flag = new int[nums.length];
		dfs(ans, tmp, nums, flag);
		return ans;
	}

	public void dfs(List<List<Integer>> ans, List<Integer> tmp, int[] nums, int[] flag) {
		if(tmp.size() == nums.length) {
			System.out.println(tmp);
			ans.add(new ArrayList<Integer>(tmp));
		}
		int len = nums.length;
		for(int i = 0; i < len; i++) {
			if(flag[i] == 0) {
				flag[i] = 1;
				tmp.add(nums[i]);
				dfs(ans, tmp, nums, flag);
				flag[i] = 0;
				tmp.remove(tmp.size()-1);
			}
		}
    }

}
```
