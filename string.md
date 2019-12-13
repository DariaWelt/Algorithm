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
```

## Minimum Window Substring
https://leetcode.com/problems/minimum-window-substring/

```C++
```

## Group Anagrams
https://leetcode.com/problems/group-anagrams/

```C++
```

## Valid Parentheses
https://leetcode.com/problems/valid-parentheses/

```C++
```

## Generate Parentheses
https://leetcode.com/problems/generate-parentheses/

```C++
```

## Valid Palindrome
https://leetcode.com/problems/valid-palindrome/

```C++
```

## Longest Palindromic Substring
https://leetcode.com/problems/longest-palindromic-substring/

```C++
```

## Palindromic Substrings
https://leetcode.com/problems/palindromic-substrings/

```C++
```

## Is Subsequence
https://leetcode.com/problems/is-subsequence/

```C++
```
