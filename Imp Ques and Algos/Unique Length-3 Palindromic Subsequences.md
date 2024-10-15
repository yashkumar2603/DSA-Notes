[Unique Length-3 Palindromic Subsequences - LeetCode](https://leetcode.com/problems/unique-length-3-palindromic-subsequences/description/)
[Unique Length-3 Palindromic Subsequences - Leetcode 1930 - Python (youtube.com)](https://www.youtube.com/watch?v=3THUt0vAFLU)
- best solution video.

```C++
class Solution {
public:
    int countPalindromicSubsequence(string s) {
        set<pair<char, char>> ans;
        set<char> left; //for right to chosen mid
        unordered_map<char, int> mp; //for right

        for(int i=0; i<s.size(); i++)
        {
            mp[s[i]]++;
        }

        for(int i=0; i<s.size(); i++) //i is the chosen mid
        {
            mp[s[i]]--;
            if(mp[s[i]]==0) mp.erase(s[i]);

            for(char c = 'a'; c<='z'; c++)
            {
                if(left.find(c)!=left.end() && mp.find(c)!=mp.end()){
                    ans.insert({s[i],c});
                }
            }
            left.insert(s[i]);
        }
        return ans.size();
    }
};
```

