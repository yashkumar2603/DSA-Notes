# Done
![[Pasted image 20240530183146.png]]
![[Pasted image 20240530183208.png]]
```C++
int main()
{
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    lli i,j,n,s,x,a,c,d,k,l;
    cin>>n;
    for(i=0;i<n;i++)
    {
        cin>>s>>x;
        c=d=0;      //s=sum,x=xor, c and d = the required pair , a=and(c&d)
        if(s<x||((s-x)%2==1))
        {
            cout<<-1<<" "<<-1<<"\n";
            continue;
        }
        a=(s-x)/2;
        for(j=0;j<32;j++)
        {
            k=(a&(1ll<<j))/(1ll<<j); //k==1 if jth bit is set in a, 0 otherwise
            l=(x&(1ll<<j))/(1ll<<j); //l==1 if jth bit is set in x, 0 otherwise
            if(k==1&&l==1)
            {
                c=d=-1;
                break;
            }
            else if(k==0&&l==1)
                d=(d|(1ll<<j));
            else if(k==1&&l==0)
            {
                d=(d|(1ll<<j));
                c=(c|(1ll<<j));
            }
        }
        cout<<c<<" "<<d<<"\n";
    }
    return 0;
}
```
