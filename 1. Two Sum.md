Given an array of integers, find two numbers such that they add up to a specific target number.

The function twoSum should return indices of the two numbers such that they add up to the target, where index1 must be less than index2. Please note that your returned answers (both index1 and index2) are not zero-based.

You may assume that each input would have exactly one solution.

**Input**: numbers={2, 7, 11, 15}, target=9

**Output**: index1=1, index2=2

**Tags**: **Array** **Hash Table**


----------
    class Solution {
    public:
    	vector<int> twoSum(vector<int>& nums, int target) {
       		vector<int> vec;
    		unordered_map<int, int> myMap;
    		int i;
    		for (i = 0; i < nums.size(); i++){
    			if (myMap.find(target - nums[i]) != myMap.end()){
    				vec.push_back(myMap[target - nums[i]] + 1);
    				vec.push_back(i + 1);
    				break;
    			}
    			myMap[nums[i]] = i;
    		}
    		return vec;
    	}
    };

* 每当遍历到一个新的数，查找是否在已经存储的数中出现。如果出现，返回在以保存字典中对应的索引值和当前数的索引值，结束。没出现继续保存。
* 时间复杂度: O(n),hash查找O(1)
* 空间复杂度:O(n)
