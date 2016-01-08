The gray code is a binary numeral system where two successive values differ in only one bit.

Given a non-negative integer *n* representing the total number of bits in the code, print the sequence of gray code. A gray code sequence must begin with 0.

For example, given *n = 2*, return `[0,1,3,2]`. Its gray code sequence is:

	00 - 0
	01 - 1
	11 - 3
	10 - 2

**Note:**

For a given *n*, a gray code sequence is not uniquely defined.

For example, `[0,2,3,1]` is also a valid gray code sequence according to the above definition.

For now, the judge is able to judge based on one instance of gray code sequence. Sorry about that.

**Tags: Backtracking**

----

	class Solution {
	public:
		vector<int> grayCode(int n) {
			vector<int> re(1,0);
			int max_value = ((unsigned)0 - 1) >> (sizeof(int) * 8 - n);
			for (int i = 1;i <= max_value;i++) {
				re.push_back(i^(i >> 1));
			}
			return re;
		}
	};

**思路：**

![Imgur](http://i.imgur.com/hrP3EJL.png)

1. 除了最高位，格雷码的位元完全上下对称。如果我们生成了n位的格雷码，可将其顺序反转，然后在两个列表的前面分别补上0和1，就可生成n+1为的格雷码。(可用bitset实现)

![Imgur](http://i.imgur.com/GKwzezO.png)

2. 自然数*n*对应的二进制数为B,其格雷码为`G(i) = B(i+1) xor B(i)`。

![Imgur](http://i.imgur.com/c0cmJwC.png)

![Imgur](http://i.imgur.com/M6XoTR0.png)

