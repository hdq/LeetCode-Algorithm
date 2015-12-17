Given a binary tree, return the postorder traversal of its nodes' values.

For example:

Given binary tree `{1,#,2,3}`,

	   1
	    \
	     2
	    /
	   3

return `[3,2,1]`.

**Note:** Recursive solution is trivial, could you do it iteratively?

**Tags:**  **Tree** **Stack**

----

	class Solution {
	public:
		vector<int> postorderTraversal(TreeNode* root) {
			vector<int> re;
			if (!root) return re;
			stack<TreeNode*> myStack;
			myStack.push(root);
			TreeNode* currNode = NULL;
			while (!myStack.empty()) {
				currNode = myStack.top();
				if (!currNode->left && !currNode->right) {
					re.push_back(currNode->val);
					myStack.pop();
					continue;
				}
				if (currNode->right) {
					myStack.push(currNode->right);
					currNode->right = NULL;
				}
				if (currNode->left) {
					myStack.push(currNode->left);
					currNode->left = NULL;
				}
			}
			return re;
		}
	};

**思路:**

　　与145题思路类似，依然是用栈的方法来实现。

　　后序遍历的顺序是`左--右--根`，那么出栈的顺序也是如此，则入栈的顺序是`根--右--左`。但是出栈的时候有一个问题，那就是出栈的条件。正确的顺序是下层节点先出栈，然后上层节点后出栈，但是怎么记录某个节点的孩子节点已经出栈了呢？只要我们在入栈的时候，当该节点的左右孩子入栈后，将节点的左右孩子置为空。算法的终止条件依然是栈为空。

![Imgur](http://i.imgur.com/aft2pSI.png)
