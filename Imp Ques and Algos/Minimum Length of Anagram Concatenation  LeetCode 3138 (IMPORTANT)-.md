[Minimum Length of Anagram Concatenation - LeetCode](https://leetcode.com/contest/weekly-contest-396/problems/minimum-length-of-anagram-concatenation/description/)
# Done
![[Pasted image 20240511083125.png|550]]

Go through the entire length of the string, the factors of the total length n only will be possible.
Now we check for each length possible, we first  take the frequency of each element in the first n/k substring. then go into all the following substrings and match the frequecies.
<font color="#f79646">THE METHOD FOR DOING THIS IS REALLY NICE</font>

```C++
class Solution {
public:
    bool isOK(string s, int len)
    {
        int n = s.size();
        int firstfreq[26] = {0};
        for(int i=0; i<len; i++)
        {
            firstfreq[s[i]-'a']++;
        }
        for(int i=len; i<n; i+=len)
        {
            int rangeFreq[26]={0};
            for(int j=i; j<i+len; j++)
            {
                rangeFreq[s[j]-'a']++;
            }
            for(int j=0; j<26; j++)
            {
                if(rangeFreq[j]!=firstfreq[j]) return false;
            }
        }
        return true;
    }

    int minAnagramLength(string s) {
        //add to hashmap and then take gcd of all the counts, the gcd is the number of ttimes t is repeated.
        int n=s.size();

        for(int i=1;i<n; i++)
        {
            if(n%i==0 && isOK(s, i))
            {
                return i;
            }
        }
        return n;
    }
};
```