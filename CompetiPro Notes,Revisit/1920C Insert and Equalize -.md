[Problem - 1902C - Codeforces](https://codeforces.com/problemset/problem/1902/C)

We have to inset an element $a_{n+1}$ in the array and it should not be equal to any number present in the array. Then, add a number x chosen by us to the numbers to make all equal to each other. 
So the x we take is equal to the gcd of difference of all the elements from the max element. 
Then we add a number $a_{n+1} = a_{max} + x.k$   If the new element becomes greater than the current max, we need to spend extra moves, since we can change x more arbitrarily than other things, lets take k=-1 and then keep on decreasing it till amax + x.k is not present in the array, then insert it and the answer becomes -
$\sum \frac{max - a_i}{x} - k$ . 

![[Pasted image 20240602012935.png]]
