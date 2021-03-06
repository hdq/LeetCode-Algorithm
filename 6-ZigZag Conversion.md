The string `"PAYPALISHIRING"` is written in a zigzag pattern on a given number of rows like this: (you may want to display this pattern in a fixed font for better legibility)

    P   A   H   N
    A P L S I I G
    Y   I   R
And then read line by line: `"PAHNAPLSIIGYIR"`

Write the code that will take a string and make this conversion given a number of rows:

    string convert(string text, int nRows);
`convert("PAYPALISHIRING", 3)` should return `"PAHNAPLSIIGYIR"`.

**Tags**: **String**

----------
	class Solution {
	public:
		string convert(string s, int numRows) {
			int len = s.length();
			if (numRows <= 1 || len < 3 || len <= numRows)
				return s;
			string str;
			int cycle = numRows * 2 - 2;
			int tmp;
			for (int i = 0; i < numRows; i++)
			{
				for (int j = i; j < len; j += cycle)
				{
					str.push_back(s[j]);
					if (i != 0 && i != (numRows - 1)) {
						tmp = j + cycle - 2 * i;
						if (tmp < len)
							str.push_back(s[tmp]);
					}
				}
			}
			return str;
		}
	};

* 对于竖列上的字符，同一行的相邻字符间的间隔是‘锯齿’形状的一个周期，`cycle = 2 * numRows - 2`。
* 相比于第一行和最后一行，中间行在这一个循环内多了一个字符。这个字符的位置（index）比它前一个字符偏移了`offset = cycle - 2 * i`。
* 时间复杂度: O(n)，空间复杂度: O(n)
