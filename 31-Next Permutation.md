Implement next permutation, which rearranges numbers into the lexicographically next greater permutation of numbers.

If such arrangement is not possible, it must rearrange it as the lowest possible order (ie, sorted in ascending order).

The replacement must be in-place, do not allocate extra memory.

Here are some examples. Inputs are in the left-hand column and its corresponding outputs are in the right-hand column.

`1,2,3 → 1,3,2`

`3,2,1 → 1,2,3`

`1,1,5 → 1,5,1`

**Tags: Array**

----------

    class Solution {
    public:
    	void nextPermutation(vector<int>& nums) {
    		if (nums.size() <= 1) return;
    		int i, j;
    		for (i = nums.size() - 2;i >= 0 && nums[i] >= nums[i + 1];i--) //反向查找第一个增序, 较小值的位置为i
    			;
    		if (i < 0) {
    			reverse(nums.begin(), nums.end()); //如果为全降序, 反转数列
    			return;
    		}
    		for (j = nums.size() - 1;j >= 0 && nums[j] <= nums[i];j--) //反向查找找到比nums[i]大的第一个数位置为j
    			;
    		swap(nums[i], nums[j]); //交换位置i和j的值
    		reverse(nums.begin() + i + 1, nums.end()); //将第i个位置以后的数列反转
    	}
    };


**思路:**

1. 对于一个序列来说，如果序列中任意一个数都比它前面的数小，即该序列是降序排列，那么按照字典序来说，这个序列是最后一个排列。因此，在一个序列中，如果其末尾由k个元素组成的子序列是降序排列，那么该子序列已经达到了局部最大值，即这k个元素形成了字典序排列的最大。
2. 如果要找到比一个排列大的下一个排列，那么对于排列大小的改变要尽可能的小。若想使得排列增长的最小，则需要去交换排列中尽可能靠后的位置，因为排列的位置越靠后就意味着对于排列的大小的影响越小。比如，排列`1 2 3 4`，交换`3`和`4`明显比交换`2`和`4`或者`2`和`3`与原排列相比所带来的改变更小，或者说`1 2 4 3`小于`1 4 2 3`和`1 3 2 4`。
3. 那么，如1中所述，既然全降序的子序列已无增大的可能，而且交换的位置越靠后影响越小。因此，就找到了倒数k+1个元素组成的序列，该子序列是非全降序的序列，这也就意味着该子序列还有再排列的空间，直到该子序列排列为全降序为止。
4. 所以，现在需要做的就是从降序的k个元素中选取一个放到倒数第k+1个位置上(倒数第k+1个元素设为L)。不过元素的选择是有条件的，首先，该元素必须要比L大。如果比L小，就意味着交换后的序列是小于原序列的，这跟目的相悖。然后，该元素是要比L大的元素中最小的，这样才能保证得到的新序列跟原序列的差距最小。
5. 接下来，还有剩下的k-1个降序的元素还有L需要排。为了保证剩下的这些元素组成的序列是最小的，需要把它们按照升序排列。即比L大的按升序依次放到L的后面，比L小的按升序依次放到L的前面。而对于程序的实现上，恰好是交换L和比L大的元素中最小的，并将这k个元素组成的序列反转。
6. 简而言之，整个操作步骤为:
	1. 反向查找第一个增序，设较小值的位置为i
	2. 反向查找找到比nums[i]大的第一个数，设位置为j，交换位置i和j的值
	3. 将第i个位置以后的数列反转


![Imgur](http://i.imgur.com/FhxVt8Z.png)
