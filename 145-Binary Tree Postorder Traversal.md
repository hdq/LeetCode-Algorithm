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

**思路1:**

后序遍历的顺序是`左--右--根`，如果我们更改一下前序遍历，把它变成`根--右--左`，然后再将结果反向，就成了`左--右--根`，得到最终结果。

----

	class Solution {
	public:
	    vector<int> postorderTraversal(TreeNode *root) {
	        stack<TreeNode*> nodeStack;
	        vector<int> re;
	        if(root==NULL) return re;
	        nodeStack.push(root);
	        while(!nodeStack.empty()) {
	            TreeNode* node= nodeStack.top();  
	            re.push_back(node->val);
	            nodeStack.pop();
	            if(node->left)
	            nodeStack.push(node->left);
	            if(node->right)
	            nodeStack.push(node->right);
	        }
	        reverse(re.begin(),re.end());
	        return re;
	    }
	};


**思路2:**

与145题思路类似，依然是用栈的方法来实现。前序遍历的时候，对于栈顶的元素是直接访问的，但是后序遍历需要知道其左右子树都被访问了以后，才能访问该节点。因此，我们需要一个变量来记录最后一个pop出来的节点，我们称之为`last_pop`。

* 如果栈顶元素有左子树，且`last_pop != top->left`，（`last_pop != top->right`如果有右子树的话），说明左子树还没有被遍历，那么将`top->left`入栈；
* 如果栈顶元素有右子树，且`last_pop != top->right`，（`top->left == NULL`或者`last_pop == top->left`），说明左子树已经被遍历，右子树还没有被遍历，那么将`top->right`入栈；
* 否则，要么是栈顶元素左右子树为空，即是叶子节点，则直接pop；要么是左右子树都已经被遍历，直接pop；

----

	class Solution {
	public:
	    vector<int> postorderTraversal(TreeNode *root) {
	        vector<int> re;
	        if (!root) return re;
	        stack<TreeNode*> s;
	        s.push(root);
	        TreeNode* last_pop = root;
	        TreeNode* top = NULL;
	        while (!s.empty()) {
	            top = s.top();
	            if(top->left && last_pop != top->left && last_pop != top->right)
	                s.push(top->left);
	            else if(top->right && last_pop != top->right && (top->left == NULL || last_pop == top->left))
	                s.push(top->right);
	            else{
	                re.push_back(top->val);
	                last_pop = top;
	                s.pop();
	            }
	        }
	        return re;
	    }
	};

**PS：中序遍历**

* 如果栈顶元素有左子树，则将`top->left`入栈，内循环直到左子树为空；
* 然后访问栈顶元素，然后pop栈顶元素；
* 如果栈顶元素有右子树，则再将右孩子入栈；否则，一直访问栈顶元素，然后pop，直到栈为空或者遇到有右孩子的节点为止。


![Imgur](http://i.imgur.com/aft2pSI.png)
