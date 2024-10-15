# Done

https://leetcode.com/problems/sum-of-all-subset-xor-totals/description/

Use recursion - choice of including the element or not, time complexity = $O(2^n)$ 
or use the bit manipulation approach for $O(n)$.

## Intuition

This approach is just feeling like some hacking and it's OK if you don't understand it (though I'll do my best so you can).

- First observation is that there is exactly **2^n** different subsets from our array. Let's consider one element `k` from this array. In how many subsets we will see that number? Based on the logic that for every subset we can either include element or not it's half from all subsets so **2^(n - 1)**.
- So in our sum will be exactly **2^(n - 1)** numbers which include XORing with `k` and exactly **2^(n - 1)** which don't. So let's say `k` has bit `1` at position `x`. What if all numbers in input doesn't have bit `1` at position `x`? Then we know that in all **2^(n - 1)** XORed numbers bit at position `x` will be `1`. That means that to sum this will add **(2^(x-1)) * 2^(n - 1)**.
- Okay, with case where only `k` has bit `1` at position all is easy. What if another number has bit `1` at `x` (let's now say only 1 number)? Okay, then all occasions where we previously had bit 1 we will have bit 0 and where we had bit 0 we will have bit 1. But we had bit `0` exactly in **(2^(x-1)) * 2^(n - 1)** (occasions, in which we haven't included number `k`) so now in fact NOTHING changed, we still have exactly **2^(n - 1)** with `1` at position `x` and so we still add **(2^(x-1)) * 2^(n - 1)** to our sum.
- So, from this observations all what is matter is do we have bit 1 in any of the numbers. (We will do this with binary OR ("|") which set bit 1 if ANY or BOTH operands have bit 1 in that position)
- Instead of multiplying each bit by its position (formula _(2^(x - 1)) * 2^(n - 1)_), we will simply move the bits n - 1 positions to the left (equivalent to counting the sum by hand)
This is really hard approach


```C++
class Solution {
public:
    int subsetXORSum(vector<int>& nums) {
        int result = 0;
        // Saving all "1" bits
        for (int num : nums) {
            result |= num;
        }
        // Finding the sum (equivalent to (2^(x - 1)) * 2^(n - 1) )
        return result << (nums.size() - 1);
    }
};
```