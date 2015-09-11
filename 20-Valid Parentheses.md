Given a string containing just the characters `'('`, `')'`, `'{'`, `'}'`, `'['` and `']'`, determine if the input string is valid.

The brackets must close in the correct order, `"()"` and `"()[]{}"` are all valid but `"(]"` and `"([)]"` are not.

**Tags: Stack String**


----------
	class Solution {
	public:
		bool isValid(string s) {
			stack<char> stack;
			unordered_map<char, char> map({ {'(',')'},{ '[',']' },{ '{','}' } });
			int strlen = s.size();
			if (strlen == 1)
				return false;

			int i = 0;
			while (i < strlen) {
				if (!stack.empty() && map[stack.top()] == s[i])
					stack.pop();
				else
					stack.push(s[i]);

				i++;
			}
			if (!stack.empty())
				return false;
			return true;
		}
	};

* 栈为空时，字符入栈；
* 栈顶字符与新来字符不匹配时，新来字符入栈；
* 栈顶字符与新来字符匹配时，栈顶字符出栈；
* 判别：最终栈是否为空，若为空则合法，否则不合法。
* 时间复杂度：O(n)，空间复杂度：O(n)
