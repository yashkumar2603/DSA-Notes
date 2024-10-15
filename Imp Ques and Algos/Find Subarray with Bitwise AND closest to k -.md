# Done too hard
The idea is that we use the 2 pointer sliding window approach.
The AND is a non-increasing function, so as we include more elements, the AND will only decrease(or constant), so we can use this to shift the left pointer inwards.
Now, the major issue is that, if we have to remove an element from the current and, it ain't that simple nigga
So, we maintain a vector of bits, whenever we see a 0 in the bits, we increment that position by 1 in the vector. as it will make the and 0 at that bit continuously. Now if a position doesn't have any 0, add that position decimal and get the current and.
For deletion, just decrement the positions of zeros from the deleted element.

```C++
class Solution {
public:
    // bit count 0's
    int calculateWindow(vector<int>& bit){
        int ans = 0;
        for(int i=0; i<32; i++){
            ans += (1<<i) * (bit[i] == 0);
        }
        return ans;
    }

    void addElement(vector<int>& bit, int el){
        for(int i=0; i<32; i++){
            if( !((el>>i) & 1) )
                bit[i]++;
        }
    }

    void subtractElement(vector<int>& bit, int el){
        for(int i=0; i<32; i++){
            if( !((el>>i) & 1))
                bit[i]--;
        }
    }

    int minimumDifference(vector<int>& nums, int k) {
        int n = nums.size(), minDiff = INT_MAX;

        vector<int> bit(32, 0);
        int i=0, j=0, rangeAnd=0;
        while(j<n){
            addElement(bit, nums[j]);
            rangeAnd = calculateWindow(bit);
            minDiff = min(minDiff, abs(rangeAnd-k));

            while(rangeAnd<k && i<j){
                subtractElement(bit, nums[i]);
                rangeAnd = calculateWindow(bit);
                minDiff = min(minDiff, abs(rangeAnd-k));
                i++;
            }

            j++;
            if(minDiff == 0) return 0;
        }

        return minDiff;
    }
};
```

