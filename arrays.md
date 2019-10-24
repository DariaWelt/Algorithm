# Arrays
+ [Triple Sum](#triple-sum)
+ [Two Sum](#two-sum)
+ [Subarray Sum Equals K](#subarray-sum-equals-k)

# Two Sum
https://leetcode.com/problems/two-sum/submissions/

Time complexity : O(n^2) 
Space complexity : O(1)
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

HASH TABLE
Time complexity : O(n log(n))
Space complexity : O(n)
```C++
#include <map>
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        map<int,int> HashMap;
        map<int,int> :: iterator searchNum;
        for (size_t i = 0; i < nums.size(); ++i){
            searchNum = HashMap.find(target - nums[i]);
            if (searchNum != HashMap.end())
                return {searchNum->second, i};
            HashMap[nums[i]] = i; 
        }
        return {0};
    }
};
```

## Triple Sum
https://leetcode.com/problems/3sum/

Time complexity : O(n^2)
Space complexity : O(n)
```C++
#include <algorithm>

class Solution {
public:
    vector<vector<int>> threeSum(vector<int>& nums) {
        sort(nums.begin(), nums.end());
        vector<vector<int>> solutionSet;
        if (nums.size() < 3)
            return solutionSet;
        size_t second;
        for (size_t i = 0; i < nums.size() - 2; ++i) {
            second = i + 1;
            size_t third = nums.size() - 1;
            while (second < third) {
                if (nums[i] + nums[second] == -nums[third]) {
                    solutionSet.push_back({ nums[i], nums[second], nums[third] });
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
## Subarray Sum Equals K
https://leetcode.com/problems/subarray-sum-equals-k/solution/

Time complexity : O(n^2)
Space complexity : O(1)
```C++
#include <algorithm>
class Solution {
public:
    int subarraySum(vector<int>& nums, int k) {
        int rezult = 0, tmpSum;
        size_t i, j;
        for (i = 0; i < nums.size(); ++i) {
            for (j = i, tmpSum = 0; j < nums.size(); ++j) {
                tmpSum += nums[j];
                if (tmpSum == k)
                    ++rezult;
            }
        }
        return rezult;
    }
};
```

HASH TABLE
Time complexity : O(n log(n))
Space complexity : O(n)
```C++
#include <algorithm>
#include <map>
class Solution {
public:
  int subarraySum(vector<int>& nums, int k) {
      int sum = 0, counter = 0;
      map<int,int> HashMap;
      HashMap[0] = 1;
      for (size_t i = 0; i < nums.size(); ++i){
          sum += nums[i];
          if (HashMap.find(sum - k) != HashMap.end())
              counter += HashMap[sum - k];
          ++HashMap[sum];
      }
      return counter;
  }
};
```
