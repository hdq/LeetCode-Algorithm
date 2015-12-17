Given a binary tree, imagine yourself standing on the right side of it, return the values of the nodes you can see ordered from top to bottom.

For example:

Given the following binary tree,

	   1            <---
	 /   \
	2     3         <---
	 \     \
	  5     4       <---

You should return `[1, 3, 4]`.

**Tags:** **Tree**, **Depth-first Search**, **Breadth-first Search**


----

	class Solution {
	public:
		vector<int> rightSideView(TreeNode* root) { //BFS
			vector<int> re;
			if (!root) return re;
			queue<TreeNode*> myQueue;
			myQueue.push(root);
			TreeNode* currNode = NULL;
			TreeNode* endNode = root; // the last node addr of one level
			while (!myQueue.empty()) {
				currNode = myQueue.front();
				myQueue.pop();
				if (currNode->left) myQueue.push(currNode->left);
				if (currNode->right) myQueue.push(currNode->right);
				if (currNode == endNode) {
					re.push_back(currNode->val);
					endNode = myQueue.empty() ? endNode : myQueue.back();
				}
			}
			return re;
		}
	};

**思路:**

　　此题的意思是要找到树每层的最后一个节点。直观的想法是，把每层的节点依次遍历，找到最后一个节点，然后放到结果列表里。因此可以采用BFS。BFS是用队列实现的，显然根节点是第一层的最后一个节点。关键在于知道队列里哪个节点是该层的最后一个节点。根据BFS的实现方法，当上一层的最后一个节点出栈时，首先会将该节点的左孩子、右孩子入栈，如果其左孩子和右孩子存在的话。那么完成之后，就意味着上一层的节点已全部出队，下一层的节点已全部入队。因此现在队列中的最后一个元素则是该层的最后一个元素。当BFS运行完毕以后，结果已经全部存入vector中。

![Imgur](http://i.imgur.com/L5v7Vbw.png)
