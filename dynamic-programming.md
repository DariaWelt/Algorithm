# Dynamic programming
+ [Longest Common Subsequence](#longest-common-subsequence)

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
