![[Pasted image 20240511084332.png]]
[Minimum Number of Operations to Make Word K-Periodic - LeetCode](https://leetcode.com/contest/weekly-contest-396/problems/minimum-number-of-operations-to-make-word-k-periodic/description/)

In this problem, we simply use the frequency of the most frequent substring in the whole string and the total number of substrings will be k.
Then, the number of operations i will have to perform will be n/k-maxfrequency. as i will replace every other substring with the one having the maximum frequency.
	To get the frequency we use the `s.substr(i, k)` function 

```C++
int minimumOperationsToMakeKPeriodic(string word, int k) {
        int n=word.size();
        unordered_map<string, int> mp;
        int mx=0;
        for(int i=0; i<n; i+=k)
        {
            string s = word.substr(i, k);
            mp[s]++;
            mx=max(mx, mp[s]);
        }
        return n/k - mx;
```