Warehouse packing Problem -
We are given B number of bags, each can hold 10kg
we are given an array of some weights, we need to tell if we can fit all these into the given bags or not,
each bag can hold any number of items, but no more than 10kg in total
- solution
sort the array and then in the Bag array, keep adding continuously the weight if bag<10kg.
if we encounter an element which cant be fit at that moment, simply return false, as it cant be done fr.
```C++
bool canPack(vector<int>& weights, int B) {
    int totalWeight = 0;
    for (int w : weights) {
        if (w > 10) return false; 
        totalWeight += w;
    }
    if (totalWeight > B * 10) return false;
    
    sort(weights.rbegin(), weights.rend());
    vector<int> bags(B, 0);
    for (int w : weights) {
        bool packed = false;
        for (int& bag : bags) {
            if (bag + w <= 10) {
                bag += w;
                packed = true;
                break;
            }
        }
        if (!packed) return false;
    }
    return true;
}
```
