# Done
![[Pasted image 20240512165852.png]]


### Solution - 
![[Pasted image 20240512165910.png]]

```C++
int sieve[1000006];
bitset<1000006> counter;
vector<int> factor(int num)
{
    vector<int> fact;
    while(num>1)
    {
        fact.push_back(sieve[num]);
        int tmp = sieve[num];
        while(num%tmp == 0)
        {
            num/=tmp;
        }
    }
    return fact;
}

void prime_factorization()
{
    for(int i=2;i<1000001;i++)
    {
        if(sieve[i] == 0)
        {
            for(int j=i;j<1000001;j+=i)
            {
                sieve[j] = i;
            }
        }
    }
}

int solve(int n, int ar[])
{
    int p1=0,p2=0;
    int maxa = 0;
    counter.reset(0);

    while(p1<n)
    {
        while(p2<n)
        {
            bool boo=1;
            int tmp = ar[p2];
            vector<int> fact = factor(tmp);
            
            for(auto i:fact)
            {
                if(counter[i])
                {
                    boo=0;
                    break;
                }
            }
            
            if(boo==0)
            {
                break;
            }
            for(auto i:fact)
            {
                counter[i]=1;
            }
            p2++;
        }
        
        maxa = max(maxa,p2-p1);
        vector<int> fact = factor(ar[p1]);
        for (auto i:fact)
        {
            counter[i] = 0;
        }
        p1++;
    }
    return maxa;
}

int ar[400000],n;
signed main()
{
    IOS
    
    prime_factorization();

    int t;
    cin>>t;
    while(t--)
    {
        cin>>n;
        for(int i=0;i<n;i++)
        {
            cin>>ar[i];
        }
        cout<<solve(n,ar)<<endl;
    }
}
```