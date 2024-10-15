The goal is to take a permutation of the given array such that when adding the 2 arrays term wise, we get the maximum no. of local maximums possible, print that permutation. The array elements are from 1 to n.
so the logic is that if we try to add n-a(i) to every element, the sum on all will be n and equal, so no local maximum, and the maximum no. of local maximums will occur when we have (n+2) as the value of the maximums. The values will come by taking 1 from each side and then adding it to the max we want to make, maximums will appear on alternate indices
and the element having 1 cannot be made to (n+2) so we have to keep that as the anchor and fill all the non-alternate positions of 1 with (n+2). and then fill the rest with decreasing order, the max element gets the least and so on.

```C++
// Link :
#include <bits/stdc++.h>
#define ll long long
using namespace std;
#define all(x) (x).begin(), (x).end()
ll lcm(ll a, ll b) { return a / __gcd(a, b) * b; }
const int N = 1e5 + 10;
#define nl "\n"

static bool comp(pair<int, int> &a, pair<int, int> &b) {
    return a.first > b.first;
}

void solution() {
    // write your code here
    int n;
    cin >> n;
    vector<int> v(n);
    set<int> s;
    vector<pair<int, int>> p;
    int j;
    for (int i = 0; i < n; i++) {
        cin >> v[i];
        if (v[i] == 1)
            j = i;
        s.insert(i + 1);
    }
    int start;

    vector<int> a(n);
    for (int i = 0; i < n; i++) {
        if (i % 2 != start % 2) {
            a[i] = n - v[i] + 2;
            s.erase(a[i]);
        } else
            p.push_back({v[i], i});
    }
    sort(p.begin(), p.end(), comp);
    int k = 0;
    for (auto i : s) {
        a[p[k++].second] = i;
    }
    for (auto i : a)
        cout << i << " ";
    cout << nl;
}
int main() {
    ios_base::sync_with_stdio(0);
    cin.tie(0);
    cout.tie(0);
    int T = 1;
    cin >> T;
    while (T--) {
        solution();
    }

    return 0;
}
```

