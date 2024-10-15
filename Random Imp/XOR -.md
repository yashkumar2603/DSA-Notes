# Done
XOR of two equal numbers is 0.
and XOR of two different inputs is 1.
<font color="#4bacc6">This leads to the question of finding the only element occurring once in a twice array to be solved by just taking the XOR of the entire array.</font>
<font color="#4bacc6">XOR of any number with 0 leads to the number itself. The twice occurring elements XOR out to 0 and the once occurring element is revealed as the output to the XOR operation.</font>
![[Pasted image 20240510182103.png|500]]

<font color="#f79646">in the question where all elements are repeating twice while 2 numbers are non- repeating</font>, then take the XOR of all the numbers, we will end up with the XOR of the answers, we have to separate them now.
To do that, we will see the rightmost set bit of a^b(XOR of the 2 answers) and then find all the elements in the array with that bit set. On having these elements, we will take their XOR and XOR it with a^b, we will obtain one of a and b, then we XOR the obtained a or b with a^b to obtain the other one.

<font color="#f79646">In the question where we have to find the element that  does not repeat in an array where every element repeats k times -</font>
To solve this, we make a count array of 32 size(the number of bits in int) then we take the elements one by one and increment the values at positions of their set bits by 1.
i.e. is the current element is 2, having binary of 10 then the 0th index of the count array is increased by 0 and the 1st index is increased by 1. We keep on incrementing in the count array in this manner for every element. 
Then we go in the count array and take %k of every element and record the results, it will lead to a binary number as some elements of  the count array will be 3k and some 3k+1.
if we convert the binary obtained from these elements into decimal, we get the desired number.

XOR of numbers from 1 to N - 
there is a niche pattern in this, 
The pattern is that
```
for every number n in the range 1 to N
	if(n%4==1) XOR=1
	if(n%4==2) XOR=n+1
	if(n%4==3) XOR=0
	if(n%4==0) XOR=n

```



