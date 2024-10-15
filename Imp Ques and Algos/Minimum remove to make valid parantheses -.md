[Minimum Remove to Make Valid Parentheses - LeetCode](https://leetcode.com/problems/minimum-remove-to-make-valid-parentheses/)

```C++
class Solution {
public:
    string minRemoveToMakeValid(string s) {
        int n=s.size();
        vector<int> vis(n, 1);
        stack<int> st;
        for(int i=0; i<n; i++)
        {
            if(s[i]=='('){
                st.push(i);
            }
            else if(s[i] == ')'){  
                if(!st.empty())
                    st.pop();

                else   //invalid, too much )
                    vis[i] = 0;
            }
        }
        while(!st.empty())  //invalid, too much (
        {
            vis[st.top()]=0;
            st.pop();
        }

        string ans="";
        for(int i=0; i<n; i++)
        {
            if(vis[i]!=0) ans+=s[i];  //add only valid places
        }

        return ans;
    }
};
```