Parity of a number means, if its odd or even. 
same parity of two numbers means, both are odd and both are even.
[Problem - C - Codeforces](https://codeforces.com/contest/1899/problem/C)

To solve this, we modify Kadane's algorithm so that we add one more checking condition, the one in the problem, which says us that no 2 consecutive elements in the chosen subarrays should have elements of the same parity.

Code - 
```C++
 int n;
cin >> n;
 
vector<ll int> a(n);
for (int i = 0; i < n; i++) {
    cin >> a[i];
}
ll int ans = -1e18, sum = 0;
for (int i = 0; i < n; i++) {
    sum += a[i];
    ans = max(ans, sum);
    if (i < n && (max(a[i], -a[i])) % 2 == (max(a[i + 1], -a[i + 1])) % 2)
        sum = 0;
    if (sum < 0)
        sum = 0;
}
 
cout << ans << nl;
```

