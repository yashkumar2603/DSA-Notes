>The `modf()` function breaks down the floating-point value x into fractional and integral parts. The signed fractional portion of x is returned. The integer portion is stored as a double value pointed to by intptr. Both the fractional and integral parts are given the same sign as x.
```C++
#include <math.h> 
#include <stdio.h> 
int main(void) { 
	double x, y, d; 
	x = -14.876; 
	
	y = modf(x, &d); 
	
	printf("x = %lf\n", x); 
	printf("Integral part = %lf\n", d);  
	printf("Fractional part = %lf\n", y); 
}   

/* Output should be similar to:  
x = -14.876000 
Integral part = -14.000000 
Fractional part = -0.876000 */
```

---

>The `rotate()` function.
>The **`rotate()` function** in C++ is used to rotate the elements’ order within a specified range. This is done in such a way that the element pointed by `middle` now becomes the first element. In other words, the rotation happens at the iterator, pointing to the `middle` element.
>
>The `rotate()` function accepts the following parameters:

- **`first`:** An iterator that points to the array’s first index or vector from where we want to rotate the elements.
    
- **`middle`:** An iterator that points to the element of the array or vector at which the rotation will be performed. This element now comes at the start of the array.
    
- **`last`:** This is an iterator that points to the last index of the array or vector until where we want to rotate the elements.
**This function rotates from right to left.**
```C++
rotate(vec.begin(), vec.begin() + 3, vec.end());

/*
Original vector: 1 2 3 4 5 6 7 8 9 
Rotated vector: 4 5 6 7 8 9 1 2 3
*/
```

---

>The expression `count(all(v), 0)` refers to C++ code and attempts to count the number of occurrences of the value 0 within the range defined by the `all(v)` expression.

