Given a binary tree, return the preorder traversal of its nodes' values.

For example:
Given binary tree `{1,#,2,3}`,

	   1
	    \
	     2
	    /
	   3

return `[1,2,3]`.

**Note:** Recursive solution is trivial, could you do it iteratively?

----

	class Solution {
	public:
		vector<int> preorderTraversal(TreeNode* root) {
			vector<int> re;
			if (!root) return re;
			stack<TreeNode*> myStack;
			myStack.push(root);
			TreeNode* currNode = NULL;
			while (!myStack.empty()) {
				currNode = myStack.top();
				re.push_back(currNode->val);
				myStack.pop();
				if (currNode->right) myStack.push(currNode->right);
				if (currNode->left) myStack.push(currNode->left);
			}
			return re;
		}
	};

**思路:**

无论是前序、中序还是后序遍历，都可以用辅助栈`(stack)`去实现。

当pop节点时访问该节点。因为前序遍历的顺序是`根--左--右`，这也是我们出栈的顺序。可以先让根入栈，然后根先出栈，再让根的孩子入栈。这就构成了整个算法的思路。其终止条件为，栈为空，栈空则意味着我们所有的节点已经遍历完。

![Imgur](http://i.imgur.com/4FAqCZK.png)
