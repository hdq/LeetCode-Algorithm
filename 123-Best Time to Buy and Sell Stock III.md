Say you have an array for which the ith element is the price of a given stock on day i.

Design an algorithm to find the maximum profit. You may complete at most two transactions.

**Note:**
You may not engage in multiple transactions at the same time (ie, you must sell the stock before you buy again).

**Tags: Array, Dynamic Programming**

----

	class Solution {
	public:
		int maxProfit(vector<int>& prices) {
			if (prices.size() <= 1) return 0;
			int i;
			int re = 0;
			int *forward_dp = new int[prices.size()];
			int *back_dp = new int[prices.size()];
			forward_dp[0] = 0;
			back_dp[prices.size() - 1] = 0;

			int low = prices.front();
			for (i = 1; i < prices.size(); i++) {
				low = min(low, prices[i]);
				forward_dp[i] = max(forward_dp[i - 1], prices[i] - low);
			}

			int high = prices.back();
			for (i = prices.size() - 2; i >= 0; i--) {
				high = max(high, prices[i]);
				back_dp[i] = max(back_dp[i + 1], high - prices[i]);
			}

			for (i = 0;i < prices.size();i++) {
				re = max(re, forward_dp[i] + back_dp[i]);
			}
			return re;
		}
	};

**思路：**

其最多允许进行两次交易，还包括进行一次交易或者不交易，后者也可以看作进行两次交易，如在当天进行一次或两次买入和卖出。

若发生了两次交易，则第二次买入需在第一次卖出以后进行，以`forward_dp[i]`表示第0天到第i天的最大收益，`back_dp[i]`表示第i天到最后一天的最大收益，显然有`dp[i] = forward_dp[i] + back_dp[i]`，其中`dp[i]`代表总收益。

由121题可知，`forward_dp[i+1] = max(forward_dp[i], prices[i+1] - lowest)`，则`back_dp[i] = max(back_dp[i+1], highest - prices[i]`。二者得到以后，即可从前向后扫描，计算`dp[i]`，找到最大值即可。

![Imgur](http://i.imgur.com/dIMUAgN.png)
