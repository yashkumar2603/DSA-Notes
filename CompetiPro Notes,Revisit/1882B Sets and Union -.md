[Problem - 1882B - Codeforces](https://codeforces.com/problemset/problem/1882/B)

The basic premise is that, if we take any number i from the union of all elements set, and then find the union of all the sets not containing i, we have a maximum set size for sets not containing i. 
And we do this for all the elements in full union set and take the max of the received sizes. That is the answer.
now this is a generic type of problem we see, but i wasn't able to even think of the solution.

The implementation uses a vector of sets to keep track of all the elements and to get the unions properly.

```C++
int n;
cin >> n;
set<int> full;
vector<set<int>> v;
for (int i = 0; i < n; i++) {
    int k;
    cin >> k;
    set<int> ts;
    for (int j = 0; j < k; j++) {
        int a;
        cin >> a;
        full.insert(a);
        ts.insert(a); 
    }
    v.push_back(ts);
}
int ans = 0;
for (auto it : full) {
    int length = 0;
    set<int> ts;
    for (auto s : v) {
        if (s.find(it) == s.end()) {
            for (auto x : s)
                ts.insert(x);
        }
    }
    length = ts.size();
    ans = max(ans, length);
}

cout << ans << nl;
```