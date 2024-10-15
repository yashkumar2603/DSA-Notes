[Problem - D - Codeforces](https://codeforces.com/contest/1955/problem/D)

Problem on search of the number of such subarrays and stuff.

![[Pasted image 20240502173946.png]]

### Solution - 
https://youtu.be/fGQGl5Suxig?si=f-cji2eNkKUzyR1q&t=2418
See this, starts at the correct time.

The basic idea is that we have to take the subarray in the array A of length m and then take the frequency of every element there. We will already have the required frequencies of the elements of b.
The number of elements of b whose frequency can be mapped is min(cntA of element, cntB of element). this is mostly to handle repeating numbers(see video).
Then we keep shifting the subarray in consideration from a ahead and on doing this, we subtract the leaving element frequency by 1 in map of A and add 1 to frequency of the new incoming element in map of A.
We check on every stage.

```C++
int n, m, k;
cin>>n>>m>>k;
 
vector<int> a(n), b(m);
 
for(auto &e: a)     cin>>e;
for(auto &e: b)     cin>>e;
 
map<int, int> cnta, cntb;
 
for(auto e: b)              cntb[e]++;  //b mapped up
for(int i=0; i<m; i++)      cnta[a[i]]++;  //first m elements taken up
 
int ans = 0;
int c = 0;
 
for(auto [e, _]: cntb)      c += min(cnta[e], cntb[e]);
 
ans += (c >= k);
 
for(int i=m; i<n; i++)
{
    cnta[a[i-m]]--;
    if(cntb[a[i-m]] > cnta[a[i-m]]) c--;  //requirement in b is more than available in a of the element.
 
    cnta[a[i]]++;
    if(cnta[a[i]] <= cntb[a[i]]) c++; //requirement in b is satisfied for atleast some occurences of the element, so increment c
 
    ans += (c >= k);
}
 
cout<<ans<<"\n";
```