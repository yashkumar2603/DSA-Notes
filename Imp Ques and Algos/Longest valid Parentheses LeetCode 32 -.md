[Longest Valid Parentheses - LeetCode](https://leetcode.com/problems/longest-valid-parentheses/description/)
# Done
The implementation is through stacks.

```C++
class Solution {
public:
    int longestValidParentheses(string s) {
        int n=s.length();
        stack<int> st;
        st.push(-1);
        int maxLen=0;
        for(int i=0;i<n;i++){
            if(s[i]=='('){
                st.push(i);
            }
            else{
                st.pop();
                if(st.empty()){
                    st.push(i);
                } else{
                    int len=i-st.top();
                    maxLen=max(len,maxLen);
                }
            }
        }
        return maxLen;
    }
};
```
