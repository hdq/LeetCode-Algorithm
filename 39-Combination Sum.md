Given a set of candidate numbers **(C)** and a target number **(T)**, find all unique combinations in **C** where the candidate numbers sums to **T**.

The **same** repeated number may be chosen from **C** unlimited number of times.

**Note:**

- All numbers (including target) will be positive integers.

- Elements in a combination (a1, a2, … , ak) must be in non-descending order. (ie, a1 ≤ a2 ≤ … ≤ ak).

- The solution set must not contain duplicate combinations.


For example, given candidate set `2,3,6,7` and target `7`, 
A solution set is: 

`[7] `

`[2, 2, 3]`

**Tags: Array, Backtracking**

----------
    
    class Solution {
    public:
    	vector<vector<int>> combinationSum(vector<int>& candidates, int target) {
    		vector<vector<int>> re;
    		if (candidates.empty()) return re;
    
    		sort(candidates.begin(), candidates.end());
    
    		vector<int> comVec;
    		backtrack(candidates, re, comVec, target, 0);
    		return re;
    
    	}
    	void backtrack(vector<int>& candidates, vector<vector<int>>& re, vector<int>& comVec, int target, int i) {
    		if (target == 0) {
    			re.push_back(comVec);
    			return;
    		}
    		for (;i < candidates.size() && target >= candidates[i];i++) {
    			comVec.push_back(candidates[i]);
    			backtrack(candidates, re, comVec, target - candidates[i], i);
    			comVec.pop_back();
    		}
    	}
    };


**思路:**

1. 题目是让我们得到和为所给目标值的候选子集，且为多重集，对于候选元素个数不限。而通过选取候选集里的元素去不断接近目标值的过程是一个不断试验的过程。为了能够得到全部可能的结果，试验的方法需要按一个特定的顺序，以保证不会漏掉或者重复。因此候选元素的选择应该按照递增或者递减的顺序，我们以递增为例。
2. 因而我们很自然的想到可以用递归的方法去做，不断的减小问题的规模，而且子问题是完全独立的。按照候选元素选取的原则，优先选取数值小的元素。说到递归，就分为两部分：第一部分是递归停止条件，第二部分是子问题划分。显然，该问题的递归停止条件就是`target <= 0`，当`target = 0`时说明找到问题的一个解，当`target < 0`时说明元素选取已不符合要求。第二个问题就是子问题拆分。很直观的想法就是，我们按照规则从中选取了一个数，然后递归给下一层去处理剩下的问题。当下一层处理完跳出以后，就说明当前选取的这个元素的解空间已经处理完，再按照规则选择下一个元素，接着递归进去寻找可行解。需要注意的是，递归到下一层的时候，初始元素的选择是有要求的，它的值必须要大于等于当前选取的元素的值，以保证我们生成的试验的顺序不会产生重复。
3. 简而言之，递归的步骤如下：

	    recursion (target, combination) {
    		if (target == 0)
    			return combination;
    		for i in candidates:
    			add new i to combination;
				recursion(target - i, combination);
				remove i from combination;
    	}




![Imgur](http://i.imgur.com/NRmzJJz.png)
