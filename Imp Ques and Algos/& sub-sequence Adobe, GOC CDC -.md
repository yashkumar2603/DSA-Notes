# Done
![[Pasted image 20240511181108.png|725]]
### Solution - 
![[Pasted image 20240511181140.png]]
```C++
void solve() {
    int n; cin >> n;
    vector<int> cnt(32, 0);
    for(int i = 0; i < n; ++i) {
        int x; 
        cin >> x; 
        for(int j = 0; j < 31; ++j) {
            if((x >> j) & 1) cnt[j]++;
        }
    }
    cout << *max_element(cnt.begin(), cnt.end());
}
```