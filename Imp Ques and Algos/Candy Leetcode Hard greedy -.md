# Intuition

We create 2 vectors left and right .  
In one iteration we iterate from left and in on iteration towards right.  
In the end we take maximum of left and right.

# Approach

1. We maintain two arrays, left and right, to track the number of candies to be given to each child from the left and right side, respectively.
2. We iterate through the ratings to update these arrays accordingly.
3. Finally, we calculate the total number of candies needed by summing up the maximum of left[i] and right[i] for each child.

# Complexity

- Time complexity:  
    O(n), where n is the size of the ratings vector, as we traverse the vector twice independently.
- Space complexity:  
    O(n), as we use two additional arrays of size n

# Code

```cpp
class Solution {
public:
    int candy(vector<int>& ratings) {
        vector<int> left(ratings.size() , 1);
        vector<int> right(ratings.size() , 1);
        int ans = 0;
        for( int i = 1 ; i < ratings.size() ; i++ )
        {
            if(ratings[i-1] < ratings[i])
            {
                left[i] = left[i-1] +1;
            }
        }
        for( int i = ratings.size()-1 ; i > 0  ; i-- )
        {
            if(ratings[i-1] > ratings[i])
            {
                right[i-1] = right[i] +1 ;
            }
        }
        for( int i = 0 ; i < ratings.size() ; i++ )
        {
            ans = ans + max(left[i] ,right[i]);
            
        }
        return ans;
        
        
    }
};
```