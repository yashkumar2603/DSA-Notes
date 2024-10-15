[Problem - 1973B - Codeforces](https://codeforces.com/problemset/problem/1973/B)

The thing here is that we need the smallest k for which the OR of the whole subarray of size k will be equal for all subarrays. Now, to do this we need to get the OR of all the subarrays while varying the k values. Now, to do this, we use Sliding window technique. We maintain a frequency array, which stores the number of 1s at any bit in the numbers of the subsequence. Then we go ahead in the sliding window of size k. We add the frequency of 1 in the new element to the frequency array and remove the frequencies of the removed element. 
This is done, as in OR, we simply get all the bits set in the constituents. Now, counting number of places having frequency >0 is the final set bit places in the OR. 
The constraints on ai is 2^20 so we take an array of size 22 for the frequencies.
Then we just go on ahead, by saving the OR value of the 1st subarray, and comparing it with the OR value found in the subsequent subarrays.
If at any point they are not same, return false.

```C++
bool check(vector<int> &a, int k, int n) {
    vector<int> freq(22);
    for (int i = 0; i < k; i++) {
        int j = 0;
        int x = a[i];
        while (x > 0) {
            if (x % 2)
                freq[j]++;
            j++;
            x /= 2;
        }
    }
    vector<int> arr = freq;
    for (int i = k; i < n; i++) {
        int x = a[i];
        int j = 0;
        while (x > 0) {
            if (x % 2)
                freq[j]++;
            j++;
            x /= 2;
        }
        j = 0;
        x = a[i - k];
        while (x > 0) {
            if (x % 2)
                freq[j]--;
            j++;
            x /= 2;
        }
        for (int l = 0; l < 22; l++) {
            if (freq[l] > 0 && arr[l] == 0)
                return false;
            if (freq[l] == 0 && arr[l] > 0)
                return false;
        }
    }
    return true;
}

void solution() {
    // write your code here
    int n;
    cin >> n;
    vector<int> a(n);
    for (int i = 0; i < n; i++) {
        cin >> a[i];
    }
    ll low = 1;
    ll high = n;
    ll ans = n;
    while (low <= high) {
        ll mid = (low + high) / 2;
        if (check(a, mid, n)) {
            high = mid - 1;
            ans = mid;
        } else {
            low = mid + 1;
        }
    }
    cout << ans << nl;
}
```