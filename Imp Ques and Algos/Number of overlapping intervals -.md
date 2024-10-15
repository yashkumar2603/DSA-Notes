# Done
This will work flawlessly.

```C++
void overlap(vector<pair<int, int> > v)
{
    // variable to store the maximum
    // count
    int ans = 0;
    int count = 0;
    vector<pair<int, char>> data;
    int n;
    cin >> n;
    // storing the x and y
    // coordinates in data vector
    for (int i = 0; i < n; i++) {
        // pushing the x coordinate
        int l, r;
        cin >> l >> r;
        data.push_back({l, 'x'});
        // pushing the y coordinate
        data.push_back({r, 'y'});
    }
    // sorting of ranges
    sort(data.begin(), data.end());
    // Traverse the data vector to
    // count number of overlaps
    for (int i = 0; i < data.size(); i++) {
        // if x occur it means a new range
        // is added so we increase count
        if (data[i].second == 'x')
            count++; ans=max(ans,count);
        // if y occur it means a range
        // is ended so we decrease count
        if (data[i].second == 'y')
            count--, 
        // updating the value of ans
        // after every traversal
    }
    // printing the maximum value
    cout << ans << endl;
}
```