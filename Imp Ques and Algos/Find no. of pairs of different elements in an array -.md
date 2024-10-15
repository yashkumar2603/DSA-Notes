# Done
for example, if array is (1,1,2,3,4,4,5) 
then the different pairs are
1 with 2 3 2 times 4 5
2 with 2 times 1 3 2 times 4 5 (1 is already counted)
4 with 2 times 1 2 3 5 
5 with 2 times 1 2 3 2 times 4 now.

so we can just take a map and put the frequency of all the elements in it, the no. of pairs formed by it will now be $arr.size()-freq(arr(i))$.
now sum this up for all the elements and u got the total number of such pairs
in O(2n) time.