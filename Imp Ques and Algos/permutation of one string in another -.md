https://leetcode.com/problems/permutation-in-string/

The idea is that the window size will be equal to the length of the first string, we map out this length from the string and check by shifting this window on the second string.

```C++
class Solution {
public:
    bool checkInclusion(string p, string s) {
        if(p.size()>s.size()) return false;
        map<char,int>m;
        for(auto x:p) m[x]+=1;
        int k=p.size(); // size of window
        vector<int>ans;
        map<char,int>temp;
        int left=0;
        //chaching for the first k size window
        for(int i=0;i<k;i++){
            temp[s[i]]+=1;
        }
        if(m==temp) return true;
        //moving the window ahead
        for(int i=k;i<s.size();i++){
           temp[s[i]]+=1;
           if(temp[s[left]]==1) temp.erase(s[left++]);
           else temp[s[left++]]-=1;
           if(temp==m) return true;
        }
        return false;
    }
};
```
