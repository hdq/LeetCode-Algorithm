Say you have an array for which the ith element is the price of a given stock on day i.

If you were only permitted to complete at most one transaction (ie, buy one and sell one share of the stock), design an algorithm to find the maximum profit.

**Tags: Array, Dynamic Programming**

----

	class Solution {
	public:
		int maxProfit(vector<int>& prices) {
			if (prices.size() <= 1) return 0;
			int low = prices[0];
			int re = 0;
			for (int i = 1; i < prices.size(); i++) {
				low = min(low, prices[i]);
				re = max(re, prices[i] - low);
			}
			return re;
		}
	};
	
**思路：**

设`dp[i]`为到第i天为止的最大收益，则显然有`dp[i+1] = max(dp[i], prices[i+1] - lowest)`。

![Imgur](http://i.imgur.com/GjtcPXt.png)

