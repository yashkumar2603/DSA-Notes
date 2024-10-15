[[Multiset -]]

---
**When we want to save the indexes of elements before sorting and then sort, use this method -**
```cpp
vector<pair<int, int>> values;
    // append the element and its index
    for (int i = 0; i < n; i++)
    {
        int x;
        cin >> x;
        values.push_back({x, i + 1});
    }
    sort(values.begin(), values.end());
```
then access any element's value by doing `values[i].first`, original index by using `values[i].second`.
> can also be done using map, but this also a neat method to do.

---


