Given n pairs of parentheses, write a function to generate all combinations of well-formed parentheses.

For example, given n = 3, a solution set is:

`"((()))", "(()())", "(())()", "()(())", "()()()"`

**Tags: Backtracking String**

	class Solution {
	public:
		vector<string> generateParenthesis(int n) {
			vector<string> vec;
			generate(vec, n, n, "");
			return vec;
		}
		void generate(vector<string>& vec, int L, int R, string str) {
			if (L == 0 && R == 0) {
				vec.push_back(str);
				return;
			}
			if (L > 0) {
				generate(vec, L - 1, R, str + "(");
			}
			if (L < R) {
				generate(vec, L, R - 1, str + ")");
			}
		}
	};


----------
* 采用递归：
* L表示剩余左括号个数，R表示剩余右括号个数
* 当没有括号剩余时，打印生成的字符串
* 当左括号还有剩余时，打印左括号
* 当剩余右括号的数量大于左括号时，打印右括号
* 复杂度：`C(2n,n)-C(2n,n-2)`或`1/(n+1)*C(2n,n)`
