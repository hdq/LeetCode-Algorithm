You are given two linked lists representing two non-negative numbers. The digits are stored in reverse order and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.

**Input**: (2 ->4 ->3) + (5 ->6 ->4)

**Output**: 7 ->0 ->8

**Tags**: **Linked List**, **Math**


----------
	/**
	 * Definition for singly-linked list.
	 * struct ListNode {
	 *     int val;
	 *     ListNode *next;
	 *     ListNode(int x) : val(x), next(NULL) {}
	 * };
	 */
	class Solution {
	public:
		ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
			ListNode *l3 = new ListNode(-1); // return l3->next
			ListNode *tmp = l3;
			int carry = 0; //进位
			int sum, nodeNum;
			while (l1 != NULL || l2 != NULL){
				sum = carry;
				if (l1){
					sum += l1->val;
					l1 = l1->next;
				}
				if (l2){
					sum += l2->val;
					l2 = l2->next;
				}
				nodeNum = (sum >= 10) ? (sum - 10) : sum;
				carry = (sum >= 10) ? 1 : 0;
				tmp->next = new ListNode(nodeNum);
				tmp = tmp->next;

			}
			if (carry == 1){
				tmp->next = new ListNode(1);
			}
			return l3->next;
		}
	};

* 顺序遍历链表取对应位求和
* 求和过程中可能产生进位，需要保留
* 时间复杂度: O(n), 空间复杂度:O(n)
