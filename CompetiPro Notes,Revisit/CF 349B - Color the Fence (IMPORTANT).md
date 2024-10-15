https://codeforces.com/problemset/problem/349/B

```C++
#include <bits/stdc++.h>
using namespace std;

void solve() {
    long long v;
    cin >> v;
    vector<long long> c(10); 
    for (int i = 1; i <= 9; i++) {
        cin >> c[i];
    }

    long long min_paint = c[1];
    int min_digit = 1;
    for (int i = 2; i <= 9; i++) {
        if (c[i] <= min_paint) {
            min_paint = c[i];
            min_digit = i;
        }
    }
    if (v < min_paint) {
        cout << -1 << endl;
        return;
    }
    int max_digits = v / min_paint;
    string result(max_digits, '0' + min_digit); 
    v %= min_paint;
    // cout<<result<<'\n';
    for (int i = 0; i < max_digits; i++) {
        for (int d = 9; d > min_digit; d--) {
            if (v + min_paint >= c[d]) {
                v += min_paint - c[d];
                result[i] = '0' + d;
                break;
            }
        }
    }
    cout << result << endl;
}

int main() {
    ios_base::sync_with_stdio(0);
    cin.tie(0);
    cout.tie(0);

    solve();

    return 0;
}
```
![[Pasted image 20240525101233.png]]

