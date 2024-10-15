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


>Rounding Real Values: Given a real number x, this returns x rounded half-up to N decimal places in O(1).
>
```C++
#include <cmath> /* modf(), floor(), ceil(), pow() */
double round(double x, unsigned int N = 0) 
{ 
	double discard; 
	if (modf(x *= pow(10, N), &discard) >= 0.5) 
		return (x < 0 ? floor(x) : ceil(x)) / pow(10,N); 
	return (x < 0 ? ceil(x) : floor(x)) / pow(10,N);
}
```

# Partitions of Integers - 
**An integer partition of n is an unordered set of positive integer which adds up to n. The number of integer partitions of n with the largest element is at most k is: f(n,k) = f(n-k,k)+f(n,k-1) where f(1,1) = 1 and f(n,k) = 0 if k>n or k< =0**

```C++
#define MAXN 100 // largest n or m 
long int_coefficient(n,k) // compute f(n,k) int n,m; {
	int i,j; 
	long f[[MAXN][MAXN];
	f [1][1] = 1; 
	
	for (i=0;i<=n;i++) 
		f[i][0] = 0; 
		
	for (i=1; i<=n; i++) 
		for (j=1; j<i; j++) 
			if (i-j <= 0) 
			   f[i][j] = f[i][k-1];
			else 
				f[i][j] = f[i-j][k]+f[i][k-1]; 
				
	return f[n][k]; 
}
```

# Fast Primeness detection - 

Uses Fermat's theorem.

```C++
bool isPrime(long input) {
	long cpowmod = 1; 
	long cpow; 
	long targpwr; //Take care of the special freak cases. 
	if (input==1) return false;
	if (input==2) return true;
	// The base I am choosing, two, must be relatively prime to 
	// the target. 
	if (input%2==0) return false;
	//If this is prime, then 2^p-1 will equal 1.If not, dream on. 
	targpwr = input - 1; 
	//My chosen base to start with is 2. 
	cpow = 2;
	//Now split target power into binary. a*b mod n = amodn * bmodn
	while(targpwr > 0) {
		//binary 1 
		if (targpwr % 2==1) {
			targpwr -= 1; 
			//Why it's called powermod... 
			cpowmod *= cpow; 
			cpowmod %= input;
		} 
		//Divide targpwr by 2 
		targpwr >>=1; 
		//Get the next powermod of 2. 
		cpow *= cpow; 
		cpow %= input;
	} 
	//If I'm left with 1, this is prime. 
	if (cpowmod==1) return true;
	else return false;
}
```

# Polygon Area - 
```C++
double polygon_area(vector<Point> poly) {
	double total = 0.0, val = 0.0; 
	int i, j; 
	for (i=0; i < poly.size(); i++) {
		j = (i+1) % (poly.size()); 
		val = (poly[i].x * poly[j].y) – (poly[j].x * poly[i].y);
		total += val;
	} 
	return total / 2;
}

}
int main() {
	vector<Point> poly; 
	// Points must be in CCW order 
	poly.resize(3); 
	poly[0] = Point(2,2); 
	poly[1] = Point(5,2); 
	poly[2] = Point(5,6); 
	cout << polygon_area(poly) << endl;
}
```

# Search a string in another (Boyer - Moore) - 

```C++
#include <stdio.h>
#include <string.h>

char s[80];
char p[80];
int last[128];
void compute_last()
{
    for (int i = 33; i < 128; i++)
        last[i] = 0;
    for (int j = 0; j < strlen(p); j++)
        last[p[j]] = j + 1;
}

int main()
{
    while (gets(s))
    {
        gets(p);
        int n = strlen(s);
        int m = strlen(p);
        compute_last();
        int t = 0;
        while (t <= n - m)
        {
            int j = m - 1;
            while ((j >= 0) && (p[j] == s[t + j]))
                j--;
            if (j == -1)
            {
                printf("pattern match at %d\n", t);
                t++;
            }
            else
            {
                int mismatch = (int)s[t + j];
                if (j < last[mismatch])
                    t++;
                else
                    t = t + j - last[mismatch] + 1;
            }
        }
    }
}
```

# Binary Exponentiation for big powers calculation-

Exponentiation by squaring is a general method for fast 6computation of large positive integer powers of a number. This method is also known as "square-and-multiply." The  following version computes x^n modulo m. Remove the "% m"  if you do not want the answer to be modded - but as this
causes overflow, you should switch to a bigger data type.

Complexity: O(log n) on the exponent of the computation.

```C++
#include <stdint.h> 
uint64_t mulmod(uint64_t a, uint64_t b, uint64_t m) { 
	uint64_t x = 0, y = a % m;

	for (; b > 0; b >>= 1) {
		if (b & 1) x = (x + y) % m; 
		y = (y << 1) % m;
	} 
	return x % m;
}  
uint64_t powmod(uint64_t a, uint64_t b, uint64_t m) { 
	uint64_t x = 1, y = a;

	for (; b > 0; b >>= 1) {
		if (b & 1) x = mulmod(x, y, m); 
		y = mulmod(y, y, m);
	} 
	return x % m;
}


/*** Example Usage ***/ 
#include <cassert> 
int main() {
	assert(powmod(2, 10, 1000000007) == 1024); 
	return 0;
}
```

# Finding the digits of a number and manipulating them - 
#### Use a string to take the input, then its all much easier - 

```C++
string x;
cin >> x;
    
for (auto &digit : x)
{
	//conditions 
    if (digit > '4')
            digit = '9' - digit + '0';
}

if (x.front() == '0') x.front() = '9';  //start and end of the number can be accessed easily.

cout << x << endl;
```

# Convert Character to integer - 
```C++
// C++ program to convert
// char to int (integer value) using typecasting

#include <iostream>
using namespace std;

int main()
{
    char ch = '5';

    // Subtracting 48 will produce desired results
    cout << int(ch) - 48 << "\n";
    
    // Also subtracting '0' will result in same output
    cout << int(ch - '0');
    return 0;
}
```
