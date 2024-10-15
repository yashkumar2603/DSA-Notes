https://leetcode.com/problems/word-break/description/

Asked frequently and in many companies - very famous and important problem.
# Approach - Dynamic Programming

The Dynamic Programming approach provides an efficient way to solve the word break problem by building up a solution iteratively. Here's a step-by-step description:

1. **Initialization**: We initialize a boolean array `dp` of length (n+1), where (n) is the length of the string `s`. The entry `dp[i]` will be `True` if there exists a word in the dictionary that ends at index (i-1) in the string `s`. We set `dp[0]` to `True` since an empty string can always be segmented.
    
2. **Determine Maximum Word Length**: We find the maximum length of a word in the dictionary using `max_len = max(map(len, wordDict))`. This helps us in reducing unnecessary iterations.
    
3. **Iterate Through the String**: We iterate through the string from index 1 to (n) (inclusive) and for each index `i`, we iterate from index (i-1) down to (i - \text{max_len} - 1) (or -1, whichever is larger).
    
4. **Check for Segmentation**: For each `j` in the range, we check if `dp[j]` is `True` and if the substring `s[j:i]` is in `wordDict`. If both conditions are met, we set `dp[i]` to `True` and break out of the inner loop. This means that there exists a valid segmentation ending at index (i-1).
    
5. **Result**: Finally, we return `dp[n]`, which will be `True` if the entire string can be segmented into words from the dictionary.
    

## Example:

Consider the example with `s = "leetcode"` and `wordDict = ["leet","code"]`. Here's how the algorithm proceeds:

- **Initialization**: `dp = [True, False, False, False, False, False, False, False, False]`.
- **Determine Maximum Word Length**: `max_len = 4`.
- **Iterate Through the String**:
    - When `i = 4`, the loop finds that `dp[0]` is `True` and `"leet"` is in the dictionary, so `dp[4]` is set to `True`.
    - When `i = 8`, the loop finds that `dp[4]` is `True` and `"code"` is in the dictionary, so `dp[8]` is set to `True`.
- **Result**: `dp[8]` is `True`, so the function returns `True`.

The use of dynamic programming ensures that we are not recomputing solutions to subproblems, and the consideration of the maximum word length helps in avoiding unnecessary iterations, making this approach both elegant and efficient.

# Complexity

- Time complexity: ( O(n * m) ), where ( n ) is the length of the string and ( m ) is the maximum length of a word in the dictionary.
- Space complexity: ( O(n) )

```C++
class Solution {
public:
    bool wordBreak(std::string s, std::vector<std::string>& wordDict) {
        int n = s.size();
        vector<bool> dp(n + 1, false);
        dp[0] = true;
        int max_len = 0;
        for (const auto& word : wordDict) {
            max_len = max(max_len, static_cast<int>(word.size()));
        }

        for (int i = 1; i <= n; i++) {
            for (int j = i - 1; j >= max(i - max_len - 1, 0); j--) {
                if (dp[j] && find(wordDict.begin(), wordDict.end(), s.substr(j, i - j)) != wordDict.end()) {
                    dp[i] = true;
                    break;
                }
            }
        }

        return dp[n];
    }
};
```