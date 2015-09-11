Write a function to find the longest common prefix string amongst an array of strings.
 
**Tags: String**


----------
	class Solution {
	public:
		string longestCommonPrefix(vector<string>& strs) {
			int i, j;
			int minLen;
			int strLen;
			int size = strs.size();
			char c;
			bool flag;

			if (size == 0)
				return "";

			minLen = strs[0].size();
			for (i = 1;i < size;i++) {
				strLen = strs[i].size();
				if (strLen < minLen)
					minLen = strLen;
			}

			for (j = 0;j < minLen;j++) {
				flag = false;
				c = strs[0][j];
				for (i = 1;i < size;i++) {
					if (strs[i][j] != c) {
						flag = true;
						break;
					}
				}
				if (flag)
					break;
			}
			return strs[0].substr(0, j);
		}
	};

* 找到最短的字符串长度minLen
* 遍历每个字符串的第i个位置，遇到不同字符时退出
* 空间复杂度： O(1)， 时间复杂度O(n)

