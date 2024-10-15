[Problem - D - Codeforces](https://codeforces.com/contest/1899/problem/D)
![[Pasted image 20240509191926.png]]

Essentially they are asking that for what values of i,j such that i< j and 
$\frac{2^{a_j}}{a_j} = \frac{2^{a_i}}{a_i}$ .
This is true only when $a_i=1$ and $a_j=2$ or $a_i=2$ and $a_j=1$.
so we just have to find that for $i<j$ how many such i j we can find.

```C++
int n;
cin>>n;

vector<ll int> a(n);
cin>>a;

ll int ans =;

map<int, int> mp;

for(autto e:a)
{
	ans+=mp[e];
	mp[e]++;
	if(e==1) ans += mp[2];
	if(e==2) ans += mp[1];
}
cout<<ans<<"\n";
```
