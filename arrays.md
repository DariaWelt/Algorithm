# Arrays
+[Triple Sum](#triple-sum)
+[Two Sum](#two-sum)

# Two Sum
https://leetcode.com/problems/two-sum/submissions/
```C++
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        vector<int> rezult;
        for (size_t i = 0; i < nums.size(); ++i){
            for(size_t j = i + 1; j < nums.size(); ++j){
                if (nums[i] + nums[j] == target){
                    rezult.push_back(i);
                    rezult.push_back(j);
                    return rezult;
                }
            }
        }
        return rezult;
    }
};
```

## Triple Sum
https://leetcode.com/problems/3sum/
```C++
#include <algorithm>

class Solution {
public:
  vector<vector<int>> threeSum(vector<int>& nums) {
    sort(nums.begin(), nums.end());
    vector<vector<int>> solutionSet;
    if (nums.size() < 3)
      return solutionSet;
    size_t second, third = nums.size() - 1;
    for (size_t i = 0; i < third - 1; ++i) {
      second = i + 1;
      third = nums.size() - 1;
      while (second < third) {
        if (nums[i] + nums[second] == -nums[third]) {
          vector<int> tmp = { nums[i], nums[second], nums[third] };
          solutionSet.push_back(tmp);
          while (second < third && nums[second] == nums[second + 1]) second++;
          while (second < third && nums[third] == nums[third - 1]) third--;
          ++second;
          --third;
        }
        else if (nums[i] + nums[second] < -nums[third])
          ++second;
        else
          --third;
      }
      while ((i < nums.size()-1) && (nums[i] == nums[i + 1])) ++i;
    }
    return solutionSet;
  }
};
```
