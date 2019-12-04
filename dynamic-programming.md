# Dynamic programming
+ [Climbing Stairs](#climbing-stairs)
+ [Longest Common Subsequence](#longest-common-subsequence)
+ [Unique Paths](#unique-paths)
+ [Jump Game](#jump-game)

## Climbing Stairs
https://leetcode.com/problems/climbing-stairs/
```C++
int climbStairs(int n) {
    if (n < 2)
        return n;
    int first = 0, second = 1;
    while (n--){
        first += second;
        swap(first, second);
    }
    return second;
}
 ```

## Longest Common Subsequence
https://leetcode.com/problems/longest-common-subsequence/

Space O(nm)

```C++
class Solution {
public:
    int longestCommonSubsequence(string text1, string text2) {
        if (!text1.length() || !text2.length())
            return 0;
        int n = text1.length();
        int m = text2.length();
        vector<vector<int>> lcs(n + 1, vector<int>(m + 1));
        
        for (size_t i = 1; i <= n; ++i) {
            for (size_t j = 1; j <= m; ++j) {
                if (text1[i - 1] == text2[j - 1])
                    lcs[i][j] = lcs[i - 1][j - 1] + 1;
                else 
                    lcs[i][j] = max(lcs[i][j - 1], lcs[i - 1][j]);
            }
        }
        return lcs[n][m];
    }
};
```

optimization (instead of array [M][N] we use array [max(M, N)] )
```C++
class Solution {
public:
    int longestCommonSubsequence(string text1, string text2) {
        if (!text1.length() || !text2.length())
            return 0;
        if (text1.length() < text2.length()) {
            string tmp = text1;
            text1 = text2;
            text2 = tmp;
        }
        
        int m = text1.length();
        int n = text2.length();
        vector<int> lcs(n + 1,0);
        int tmp;
        
        for (size_t i = 1; i <= m; ++i) {
            int diag = 0;  //for item with same previous end number (lcs[i-1][j-1])
            for (size_t j = 1; j <= n; ++j) {
                tmp = lcs[j];
                if (text1[i - 1] == text2[j - 1])
                    lcs[j] = diag + 1;
                else {
                    if (lcs[j] < lcs[j - 1])
                        lcs[j] = lcs[j - 1];
                }
                diag = tmp;
            }
        }
        return lcs[n];
    }
};
```

## Unique Paths
https://leetcode.com/problems/unique-paths/


with memory optimization (instead of array [M][N] we use array [min(M, N)] )
```C++
int uniquePaths(int m, int n) {
    if (m > n){
        swap(m,n);
    } 
    vector<int> diag(m, 0);
    diag[m-1] = 1;
    for (int i = 0; i < (m - 1) + (n - 1); ++i) { //we step up throw grid almost twise
        for (int j = 0; j < m - 1; ++j) {
            diag[j] += diag[j+1];
        }
    }
    return diag[0];
}
```

## Jump Game
https://leetcode.com/problems/jump-game/submissions/

1)Using helping array of condition (bad or good this point is)
Time Complexity = O(n^2)
Space Complexity = O(n)

```C++
bool canJump(vector<int>& nums) {
    vector<int> condition (nums.size(),0);
    condition[nums.size()-1] = 1;
    for (int i = nums.size() - 1; i > 0; --i) {
        for (int j = 0; j < nums[i-1] && i + j < nums.size(); ++j) {
            if (condition[i-1] == 0){
                condition[i-1] += condition[i+j];
            }
        }
    }
    return condition[0] == 1;
}
```

2)using only one position - lower good point
Time Complexity = O(n)
Space Complexity = O(1)

```C++
 bool canJump(vector<int>& nums) {
    int possibPos = nums.size()-1;
    for (int curPos = nums.size()-2; curPos >=0; --curPos) {
        if (curPos + nums[curPos] >= possibPos)
            possibPos = curPos;
    }
    return possibPos == 0;
}
```

```C++
```

```C++
```

```C++
```

```C++
```


```C++
```
