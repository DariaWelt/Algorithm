## Intervals
+ [Non-overlapping Intervals](#non-overlapping-intervals)
+ [Merge Intervals](#merge-intervals)
+ [Insert Interval](#insert-interval)

## Non-overlapping Intervals
https://leetcode.com/problems/non-overlapping-intervals/

```C++
#include <algorithm>
class Solution {
public:
    static bool cmpIntervals (vector<int>& a, vector<int>& b) {
        return a[0] < b[0];
    }
    int eraseOverlapIntervals(vector<vector<int>>& intervals) {
        if (intervals.size() == 0)
            return 0;
        sort(intervals.begin(), intervals.end(),cmpIntervals);
        int currentEnd = intervals[0][1], counter = 0;
        for (size_t i = 1; i < intervals.size(); ++i) {
            if (currentEnd > intervals[i][0]){
                ++counter;
                if (currentEnd < intervals[i][1])
                    continue;
            }
            currentEnd = intervals[i][1];
        }
        return counter;
    }
};
```
## Merge Intervals
https://leetcode.com/problems/merge-intervals/

```C++
#include <algorithm>
class Solution {
public:
    vector<vector<int>> merge(vector<vector<int>>& intervals) {
        sort(intervals.begin(), intervals.end(), [](const vector <int> &a, const vector <int> &b) {return a[0] < b[0]; });
        vector<vector<int>> rezult;
        for (size_t i = 0, j = 0; j < intervals.size() && i < intervals.size();++i){
            rezult.push_back(intervals[j]);
            ++j;
            while (j < intervals.size() &&rezult[i][1] >= intervals[j][0]){
                if (rezult[i][1] < intervals[j][1])
                    rezult[i][1] = intervals[j][1];
                ++j;
            }
        }
        return rezult;
    }
};
```
## Insert Interval
https://leetcode.com/problems/insert-interval/

```C++
class Solution {
public:
  vector<vector<int>> insert(vector<vector<int>>& intervals, vector<int>& newInterval) {
    if (intervals.size() == 0)
      return { newInterval };
    vector<vector<int>> result;
    size_t i = 0;
    for (; i < intervals.size() && intervals[i][1] < newInterval[0]; ++i)
      result.push_back(intervals[i]);
    if (i != intervals.size() && intervals[i][0] <= newInterval[1]) {
      newInterval[0] = min(intervals[i][0], newInterval[0]);
      while (i < intervals.size() - 1 && intervals[i + 1][0] <= newInterval[1])
        ++i;
      newInterval[1] = max(intervals[i][1], newInterval[1]);
      ++i;
    }
    result.push_back(newInterval);
    for (; i < intervals.size(); ++i)
      result.push_back(intervals[i]);
    return result;
  }
};
```
