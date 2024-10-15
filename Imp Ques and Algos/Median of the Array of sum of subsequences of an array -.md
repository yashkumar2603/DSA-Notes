![[Pasted image 20240512182309.png]]

## Solution - 

![[Pasted image 20240512182250.png|818]]

```C++
#include <bits/stdc++.h>
using namespace std;
int main()
{
    int n;
    cin>>n;
    int a[n+1];
    int sum=0;
    for(int i=0;i<n;i++)
    {
        cin>>a[i];
        sum+=a[i];
    }
    bitset<4000001> dp;
    dp.set(0);
    for(int i=0;i<n;i++)
        dp|=dp<<a[i];
    int x=sum/2;
    if(sum%2!=0)
        x++;
    for(int i=x;i<=sum;i++)
        if(dp[i])
        {
            cout<<i<<endl;
            return 0;
        }
}
```