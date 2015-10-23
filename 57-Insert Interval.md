Given a set of non-overlapping intervals, insert a new interval into the intervals (merge if necessary).

You may assume that the intervals were initially sorted according to their start times.

**Example 1:**

Given intervals `[1,3],[6,9]`, insert and merge `[2,5]` in as `[1,5],[6,9]`.

**Example 2:**

Given `[1,2],[3,5],[6,7],[8,10],[12,16]`, insert and merge `[4,9]` in as `[1,2],[3,10],[12,16]`.

This is because the new interval `[4,9]` overlaps with `[3,5],[6,7],[8,10]`.

**Tags: Array, Sort**

----------

    class Solution {
    public:
    	vector<Interval> insert(vector<Interval>& intervals, Interval newInterval) {
    		vector<Interval> re;
    		int i, start, end;
    
    		if (intervals.empty()) {
    			re.push_back(newInterval);
    			return re;
    		}
    		if (newInterval.start > intervals.back().end) {
    			intervals.push_back(newInterval);
    			return intervals;
    		}
    
    		i = 0;
    		while (i < intervals.size() && intervals[i].end < newInterval.start)
    			re.push_back(intervals[i++]);
    
    		start = min(newInterval.start, intervals[i].start);
    
    		while (i < intervals.size() && intervals[i].start <= newInterval.end)
    			i++;
    
    		end = (i>0) ? max(newInterval.end, intervals[i - 1].end) : newInterval.end;
    
    		re.push_back(Interval(start, end));
    
    		while (i < intervals.size())
    			re.push_back(intervals[i++]);
    
    		return re;
    	}
    };

**思路:**

问题的关键就在于把`newInterval`放到合适的位置。显然，如果新区间在区间序列的最前或者最后，只需要插入到`intervals`的头部或者尾部就可以了。更一般的情况则是新区间和区间序列中的区间有重叠或者是在区间之间。

可大致分为如下几种情况：

    [　　　]　　[　　　]　　[　　　]
    
    　↑_↑
    
    [　　　]　　　　[　　　]　　[　　　]
    
    　　　　　↑_↑
    
    [　　　]　　[　　　]　　[　　　]
    
    　↑__________↑
    
    [　　　]　　　[　　　]　　[　　　]
    
    　　　　　↑__________↑

那么合并的结果为：左边界是`min(newInterval.start, intervals[i].start)`，右边界是`max(newInterval.end, intervals[i].end)`。

![Imgur](http://i.imgur.com/Wo0KyEq.png)
