https://atcoder.jp/contests/abc362/tasks/abc362_c
![[Pasted image 20240716214411.png]]

we start with the lower bound, sum of all L's and then keep on increaasing Xi till sum is negative, if for some Xi, the sum becomes 0, we stop there and increase it only so much that the sum is 0.
```C++
void solution() {
    ll n;
    cin >> n;
    vector<pair<ll, ll>> a(n);
    ll lb = 0, ub = 0;
    for (auto &x : a) {
        cin >> x.first >> x.second;
        lb += x.first;
        ub += x.second;
    }
    if (ub < 0 || lb > 0) {
        cout << "No" << endl;
        return;
    }
    cout << "Yes" << endl;
    ll df = -lb;
    vector<int> b;
    for (const auto &x : a) {
        const ll c = min(df, x.second - x.first);
        b.emplace_back(x.first + c);
        df -= c;
    }
    for (const auto &x : b)
        cout << x << " ";
    cout << endl;
}
```

