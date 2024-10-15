# Done
**Sweep Line Algorithm :** The idea is to represent an instance of the problem as a set of events that correspond to points in the plane. The events are processed in increasing order according to their x or y coordinates. Using a vertical line, horizontal line or radial line that is conceptually “swept” across the plane.
![[Pasted image 20240525215503.png]]

Follow the steps mentioned below to implement the idea:

- **Sort** the given set of points in ascending order of their x-coordinate. 
- We go through the points by taking a vertical line swept from left to right and maintain a value ***d***: the minimum distance between two points seen so far. 
- At each point, we find the nearest point to the left. If the distance is less than ***d***, it is the new minimum distance and we update the value of ***d***. 
- If the current point is ****(x, y)**** and there is a point to the left within a distance of less than d,  
    - the ***x coordinate*** of such a point must be between ****[x – d, x]**** and the ***y coordinate*** must be between ****[y – d, y+ d].**** 
    - Thus, it suffices to only consider points that are located in those ranges. We can achieve this search in ***O(logN)*** time by using ***set*** _***st***___.__
    - The efficiency of the algorithm is based on the fact that the region always contains only O(1) points.
- Return distance ***d*** as a final result.

Below is the implementation of the above approach:

```C++
// To find the closest pair of points
long closestPair(vector<pair<int, int> > coordinates, int n)
{
    int i;
    // Vector pair to store points on plane
    vector<pair<int, int> > v;
    for (i = 0; i < n; i++)
        v.push_back({ coordinates[i].first,
                      coordinates[i].second });
    // Sort them according to their
    // x-coordinates
    sort(v.begin(), v.end());
    // Minimum distance b/w points
    // seen so far
    long d = INT_MAX;
    // Keeping the points in
    // increasing order
    set<pair<int, int> > st;
    st.insert({ v[0].first, v[0].second });
 
    for (i = 1; i < n; i++) {
        auto l = st.lower_bound(
            { v[i].first - d, v[i].second - d });
        auto r = st.upper_bound(
            { v[i].first, v[i].second + d });
        if (l == st.end())
            continue;
        for (auto p = l; p != r; p++) {
            pair<int, int> val = *p;
            long dis = (v[i].first - val.first)
                           * (v[i].first - val.first)
                       + (v[i].second - val.second)
                             * (v[i].second - val.second);
            // Updating the minimum
            // distance dis
            if (d > dis)
                d = dis;
        }
        st.insert({ v[i].first, v[i].second });
    }
    return d;
}
```