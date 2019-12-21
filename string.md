# String
+ [Longest Substring Without Repeating Characters](#longest-substring-without-repeating-characters)
+ [LongestRepeating Character Replacement](#longest-repeating-character-replacement)
+ [Minimum Window Substring](#minimum-window-substring)
+ [Group Anagrams](#group-anagrams)
+ [Valid Parentheses](#valid-parentheses)
+ [Generate Parentheses](#generate-parentheses)
+ [Valid Palindrome](#valid-palindrome)
+ [Longest Palindromic Substring](#longest-palindromic-substring)
+ [Palindromic Substrings](#palindromic-substrings)
+ [Is Subsequence](#is-subsequence)

## Longest Substring Without Repeating Characters
https://leetcode.com/problems/longest-substring-without-repeating-characters/

```C++
int lengthOfLongestSubstring(string s) {
    string letters;
    int answ = 0;
    for (auto letter : s) {
        int pos = letters.find(letter);
        if (pos != -1){
            answ = max(answ, (int)letters.length());
            letters.erase(0, pos + 1);
        }
        letters.push_back(letter);
    }
    return max((int)letters.length(), answ);
}
```

## LongestRepeating Character Replacement
https://leetcode.com/problems/longest-repeating-character-replacement/

```C++
int characterReplacement(string s, int k) {
    int start = 0, repeating = 0;
    vector<int> count(('Z' - 'A' + 1), 0);
    int res = 0;
    for (int end = 0; end < s.size(); ++end) {
        ++count[s[end] - 'A'];
        repeating = max(repeating, count[s[end] - 'A']);
        //window length
        if ((end - start + 1) - repeating > k) {
            count[s[start] - 'A']--;
            ++start;
        }
        res = max(res, (end - start + 1));
    }
    return res;
}
```

## Minimum Window Substring
https://leetcode.com/problems/minimum-window-substring/

```C++
string minWindow(string s, string t) {
    vector<int> nums(128, 0);
    for(auto letter : t)
        nums[letter]++;
    int count = 0;
    int start = -1, minLen = s.size() + 1;
    for (int left = 0, right = 0; right < s.size(); ++right) {
        if (nums[s[right]]-- > 0) {
            ++count;
        }
        while (count == t.size()) {
            if (right - left + 1 < minLen) {
                minLen = right - left + 1;
                start = left;
            }
            if (nums[s[left]]++ >= 0) {
                --count;
            }
            ++left;
        }
    }
    return start == -1 ? "" : s.substr(start, minLen);
}
```

## Group Anagrams
https://leetcode.com/problems/group-anagrams/

```C++
vector<vector<string>> groupAnagrams(vector<string>& strs) {
    unordered_map<string, int> anagrams;
    vector<vector<string>> answer;
    for (auto word : strs) {
        string key = word;
        sort(key.begin(), key.end());
        unordered_map<string, int>::iterator mi = anagrams.find(key);
        if (mi == anagrams.end()) {
            anagrams[key] = answer.size();
            answer.push_back({word});
        } else 
            answer[mi->second].push_back(word);
    }
    return answer;
}
```

## Valid Parentheses
https://leetcode.com/problems/valid-parentheses/

```C++
bool isValid(string s) {
    stack<char> brackets;
    for (auto symbol : s) {
        if (symbol == '(' || symbol == '{' || symbol == '[')
            brackets.push(symbol);
        else {
            if (brackets.empty())
                return false;
            char tmp = brackets.top();
            brackets.pop();
            switch(tmp) {
              case '(':
                if (symbol != ')')
                    return false;
                break;
              case '{':
                if (symbol != '}')
                    return false;
                break;
              case '[':
                if (symbol != ']')
                    return false;
                break;
              default: ;
            }
        }
    }
    return brackets.empty() ? true : false;
}
```

## Generate Parentheses
https://leetcode.com/problems/generate-parentheses/

```C++
class Solution {
private:
    void reqursion(vector<string>& res, int right, int left, string s) {
        if (!left && !right) {
            res.push_back(s);
            return;
        }
        if (left > 0) 
            reqursion(res, right, left - 1, s + '(');
        if (right > 0 && right > left)
            reqursion(res, right - 1, left, s + ')');
            
    }
public:
    vector<string> generateParenthesis(int n) {
        vector<string> result;
        reqursion(result, n, n, "");
        return result;
    }
};
```

## Valid Palindrome
https://leetcode.com/problems/valid-palindrome/

```C++
bool isPalindrome(string s) {
    int right = s.length() - 1, left = 0;
    while (right >= left) {
        while (right >= left && !isalnum(s[right])) --right;
        while (right >= left && !isalnum(s[left])) ++left;
        if (right >= left && tolower(s[right]) != tolower(s[left]))
            return false;
        --right;
        ++left;
    }
    return true;
}
```

## Longest Palindromic Substring
https://leetcode.com/problems/longest-palindromic-substring/

```C++
string longestPalindrome(string s) {
    int resStart = 0;
    int max = 0;
    for (int i = 0; i < s.size();) {
        int start = i, end = i;
        while (end + 1 < s.size() && s[end] == s[end + 1]) ++end;
        i = end + 1;
        while (start - 1 >= 0 && end + 1 < s.size() && s[start - 1] == s[end + 1]) {
            --start;
            ++end;
        }
        if (end - start + 1 > max) {
            max = end - start + 1;
            resStart = start;
        }
    }
    return s.substr(resStart, max);
}
```

## Palindromic Substrings
https://leetcode.com/problems/palindromic-substrings/

```C++
int countSubstrings(string s) {
    int res = s.size();
    vector<vector<bool>> pal(s.size(), vector<bool>(s.size(), true));
    for (int len = 2; len <= s.size(); len++) {
        for (int i = 0; i <= s.size() - len; i++) {
            int j = i + len - 1;
            pal[i][j] = (s[i] == s[j]) && ((len > 2) ? pal[i+1][j-1]:true);
            if (pal[i][j]) res++; 
        }
    }
    return res; 
}
```

## Is Subsequence
https://leetcode.com/problems/is-subsequence/

```C++
bool isSubsequence(string s, string t) {
    int left = 0;
    int right = 0;
    if(s.empty())
        return true;
    while(right<t.length()){
        if(t[right]==s[left]){
            left++;
            if(left>=s.length()){
                return true;
            }
            right++;
        }
        else
            right++;
    }
    return false;
}
```
