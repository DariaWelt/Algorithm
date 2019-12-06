# Dynamic programming
+ [Knapsack problem](#knapsack-problem)
+ [Climbing Stairs](#climbing-stairs)
+ [Coin Change](#coin-change)
+ [Longest Increasing Subsequence](#longest-increasing-subsequence)
+ [Longest Common Subsequence](#longest-common-subsequence)
+ [Word Break](#word-break)
+ [Unique Paths](#unique-paths)
+ [Unique Paths II](#unique-paths-ii)
+ [Jump Game](#jump-game)
+ [Jump Game II](#jump-game-ii)
+ [House Robber](#house-robber)
+ [House Robber II](#house-robber-ii)
+ [Decode Ways](#decode-ways)
+ [Coin Change 2](#coin-change-2)
+ [N-Queens](#n-queens)
+ [N-Queens II](#n-queens-ii)

## Knapsack problem
https://stepik.org/lesson/13259/step/5?unit=3444
```C++
```

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
## Coin Change
https://leetcode.com/problems/coin-change/ 
```C++
int coinChange(vector<int>& coins, int amount) {
    if (!coins.size())
        return -1;
    vector<int> sum(amount + 1,amount + 1);
    sum[0] = 0;
    for (int i = 1; i < amount + 1; ++i) {
        for (int j = 0; j < coins.size(); ++j) {
            if (i >= coins[j]){
                sum[i] = min(sum[i], sum[i - coins[j]] + 1);
            }
        }
    }
    return sum[amount] > amount ? -1 : sum[amount];
}
```
## Longest Increasing Subsequence
https://leetcode.com/problems/longest-increasing-subsequence/
```C++
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
## Word Break
https://leetcode.com/problems/word-break/
```C++
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

## Unique Paths II
https://leetcode.com/problems/unique-paths-ii/
```C++
int uniquePathsWithObstacles(vector<vector<int>>& obstacleGrid) {
    if (obstacleGrid.back().back() == 1 || obstacleGrid.front().front() == 1)
        return 0;
    vector<long> curCol(obstacleGrid.size(),0), preCol(obstacleGrid.size(),0);
    // initialize preCol (first column)
    for(int i = 0; i < obstacleGrid.size(); ++i) {
        if(obstacleGrid[i][0] == 1) {
            break;
        }
        preCol[i] = 1;
    }
    for (int i = 1; i < obstacleGrid[0].size(); ++i) {
        bool obstacle = true;
        //we cannot reach cell (step down) if we have an obstacle in first row
        curCol[0] = obstacleGrid[0][i] == 1? 0 : preCol[0]; 
        if (curCol[0]){
            obstacle = false;
        }
        for (int j = 1; j < obstacleGrid.size(); ++j) {
            if(obstacleGrid[j][i] == 1) {
                curCol[j] = 0;
            }
            else {
                curCol[j] = curCol[j-1] + preCol[j]; 
                if(curCol[j]) {
                    obstacle = false;
                }
            }
        }
        if(obstacle)
            return 0; 
        swap(preCol, curCol);
    }
    return preCol.back();
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
## Jump Game II
https://leetcode.com/problems/jump-game-ii/
```C++
int jump(vector<int>& nums) {
    if (nums.size() <= 1)
        return 0;
    int curPos = 0, maxPos = 0, nextMax = 0;
    int count = 0;
    while (maxPos < nums.size() - 1) {
        ++count;
        for (int i = curPos; i <= maxPos; ++i) {
            nextMax = max(nextMax, i + nums[i]);
        }
        curPos = maxPos + 1;
        maxPos = nextMax;
    }
    return count;
}
```

## House Robber

https://leetcode.com/problems/house-robber
```C++
int rob(vector<int>& nums) {
    if (nums.size() == 0){
        return 0;
    }
    if (nums.size() == 1){
        return nums[0];
    }
    int first = nums[0], second = nums[1];
    for (int i = 2; i < nums.size(); ++i) {
        swap(first, second);
        int tmps = second;
        second = max(second + nums[i], first);
        first = max(first, tmps);
    }
    return max(first, second);
}
```
## House Robber II

https://leetcode.com/problems/house-robber-ii/

```C++
int rob(vector<int>& nums) {
    if (nums.size() == 0){
        return 0;
    }
    if (nums.size() == 1){
        return nums[0];
    }
    if (nums.size() == 2){
        return max(nums[0],nums[1]);
    }
    int prev1 = nums[0], cur1 = nums[1]; // 1 house have robbed
    int prev2 = nums[1], cur2 = nums[2]; // 1 house haven't robbed
    for (int i = 2; i < nums.size() - 1; ++i) {
        swap(cur1, prev1);
        int tmp = cur1;
        cur1 = max(cur1 + nums[i], prev1);
        prev1 = max(prev1, tmp);

        swap(cur2, prev2);
        tmp = cur2;
        cur2 = max(cur2 + nums[i + 1], prev2);
        prev2 = max(prev2, tmp);
    }
    return max(max(cur1, prev1), max(cur2, prev2));
}
```
## Decode Ways
https://leetcode.com/problems/decode-ways/
```C++
int numDecodings(string s) {
    if (s.length() == 0 || s[0] == '0')
            return 0;
    int first = 1;
    int second = 1;
    for (int i = 1; i < s.length(); ++i) {
        if (s[i] == '0') {
            if (s[i-1] > '2' || s[i-1] == '0')
                return 0;
        }
        if ((s[i-1] - '0') * 10 + (s[i] - '0') <= 26) {
            swap(first, second);
            if (s[i] == '0') {
                first = 0;
            }
            else {
                second += first;
            }
        }
        else {
            first = second;
        }
    }
    return second;
}
```

## Coin Change 2
https://leetcode.com/problems/coin-change-2/
```C++
int change(int amount, vector<int>& coins) {
    vector<int> combinations(amount + 1,0);
    combinations[0] = 1;
    for (int i = 0; i < coins.size(); ++i) {
        for(int j = 0; j <= amount; ++j) {
            if (j+coins[i] <= amount){
                combinations[j+coins[i]] += combinations[j];
            }
        }
    }
    return combinations[amount];
}
```

## N-Queens
https://leetcode.com/problems/n-queens/
```C++
class Solution {
private:
    bool isvalid(vector<string>& board, int row, int col, vector<int>& diag1, vector<int>& diag2, vector<int>& columns) {
        return !columns[col] && !diag1[row + col] && !diag2[row - col + board.size() - 1];
    }
    void StandQ(vector<string>& board, vector<vector<string>>& result, 
                int row, vector<int>& diag1, vector<int>& diag2, vector<int>& col) {
        if (row == col.size()){
            vector<string> var = board;
            result.push_back(var);
        } else {
            for (int i = 0; i < col.size(); ++i) {
                if (isvalid(board, row, i, diag1, diag2, col)) {
                    board[row][i] = 'Q';
                    diag1[row + i] = diag2[row - i + board.size() - 1] = col[i] = 1;
                    StandQ(board, result, row + 1, diag1, diag2, col);
                    diag1[row + i] = diag2[row - i + board.size() - 1] = col[i] = 0;
                    board[row][i] = '.';
                }
            }
        }
    }
public:
    vector<vector<string>> solveNQueens(int n) {
        vector<vector<string>> result;
        vector<int> diag1(2 * n,0);
        vector<int> diag2(2 * n,0);
        vector<int> columns(n,0);
        string s(n,'.');
        vector<string> board(n, s);
        StandQ(board, result, 0, diag1, diag2, columns);
        return result;
    }
};
```

## N-Queens II
https://leetcode.com/problems/n-queens-ii/
```C++
class Solution {
private:
    bool isvalid(int row, int col, vector<int>& diag1, vector<int>& diag2, vector<int>& columns) {
        return !columns[col] && !diag1[row + col] && !diag2[row - col + columns.size() - 1];
    }
    void StandQ(int& result, int row, vector<int>& diag1, vector<int>& diag2, vector<int>& col) {
        if (row == col.size()){
            ++result;
        } else {
            for (int i = 0; i < col.size(); ++i) {
                if (isvalid(row, i, diag1, diag2, col)) {
                    diag1[row + i] = diag2[row - i + col.size() - 1] = col[i] = 1;
                    StandQ(result, row + 1, diag1, diag2, col);
                    diag1[row + i] = diag2[row - i + col.size() - 1] = col[i] = 0;
                }
            }
        }
    }
public:
    int totalNQueens(int n) {
        int result = 0;
        vector<int> diag1(2 * n,0);
        vector<int> diag2(2 * n,0);
        vector<int> columns(n,0);
        StandQ(result, 0, diag1, diag2, columns);
        return result;
    }
};
```
