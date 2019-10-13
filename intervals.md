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
  int eraseOverlapIntervals(vector<vector<int>>& intervals) {
    if (intervals.size() == 0)
      return 0;
    int counter = 0, i = 0, j;
    sort(intervals.begin(), intervals.end(), [](const vector <int> &a, const vector <int> &b) {return a[0] < b[0]; });
    while (i < intervals.size() - 1) {
      j = i + 1;
      while (j < intervals.size() && intervals[i][1] > intervals[j][0]) {
        ++counter;
         if (intervals[i][1] - intervals[i][0] > intervals[j][1] - intervals[j][0])
          break;
        ++j;
      }
      i = j;
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

```
