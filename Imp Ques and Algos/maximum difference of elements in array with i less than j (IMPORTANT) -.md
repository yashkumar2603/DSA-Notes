max(A[j]-A[i]) when i<=j
# Done
[algorithm - Interview Question - Find the Max difference of Two elements in the Array in less than O(n^2) - the Lower element should precede the Greater element - Stack Overflow](https://stackoverflow.com/questions/73645929/interview-question-find-the-max-difference-of-two-elements-in-the-array-in-les#:~:text=Find%20the%20maximum%20difference%20between,is%2065%20%2D%203%20%3D%2062%20.)
[Maximum Difference between Two Elements such that Larger Element Appears after the Smaller Element - GeeksforGeeks](https://www.geeksforgeeks.org/maximum-difference-between-two-elements/)
```C++
int main()
{
    int n;
    cin>>n;
    for(int i=1;i<=n;i++)
        cin>>a[i];
    maxi[n]=a[n];
    for(int i=n-1;i>=1;i--)
        maxi[i]=max(maxi[i+1],a[i]);
    int ans=0;
    for(int i=1;i<=n-1;i++)
        ans=max(ans,(maxi[i+1]-a[i]));
    cout<<ans<<endl;
    return 0;
}
```