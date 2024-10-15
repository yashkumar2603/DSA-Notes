https://www.youtube.com/watch?v=_eNhaDCr6P0
https://leetcode.com/problems/longest-repeating-character-replacement/
# Done
```C++
class Solution {
public:
    int characterReplacement(string s, int k) {
        unordered_map<char, int> alphabets;
        int ans = 0;
        int left = 0;
        int right = 0;
        int maxf = 0;

        for (right = 0; right < s.size(); right++) {
            alphabets[s[right]]++;
            maxf = max(maxf, alphabets[s[right]]);

            if ((right - left + 1) - maxf >
                k) { // shift the window if the length of window-maxf>k
                // This condition ensures that we have at most k changes to any
                // character in the window.
                alphabets[s[left]] -= 1;
                left++;
            } else {
                ans = max(ans, (right - left + 1));
            }
        }

        return ans;
    }
};
```

