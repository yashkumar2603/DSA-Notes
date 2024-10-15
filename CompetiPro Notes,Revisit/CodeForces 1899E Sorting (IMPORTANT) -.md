[Problem - E - Codeforces](https://codeforces.com/contest/1899/problem/E)
Solution vid. - [Codeforces Round 909 | Video Solutions - A to G | by Ankit Ghildiyal | TLE Eliminators (youtube.com)](https://www.youtube.com/watch?v=9AMKfmiOQ5Q)

The idea is that the least element will continue reaching to the first element again and again if it is at the first position. So the location at which the least element is present is gonna become the first index of the new sorted array. 
if we take the elements that come before the least elements location, they will end up at their sorted positions automatically, we just need to check if the array after the least element is sorted or not.
The impossible case would occur when the array after the least element is not sorted.

Code - 
```C++
int n;
cin >> n;
int a[n];
int mi = INT_MAX;
int idx = n;
bool sorted = true;
for (int i = 0; i < n; i++) {
    cin >> a[i];
    if (i >= 1) {
        if (a[i] < a[i - 1])
            sorted = false;
    }
    mi = min(mi, a[i]);
}
for (int i = 0; i < n; i++) {
    if (mi == a[i]) {
        idx = i;
        break;
    }
}
 
if (sorted) {
    cout << "0" << nl;
    return;
}
int ans = idx;
 
for (int i = idx; i < n - 1; i++) {
    if (a[i] > a[i + 1]) {
        cout << "-1" << nl;
        return;
    }
}
cout << ans << nl;
```

