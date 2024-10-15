```C++
// Function to calculate sum of all proper divisors
// num --> given natural number
int divSum(int num)
{
    // Final result of summation of divisors
    int result = 0;
    if(num == 1) // there will be no proper divisor 
      return result;
    // find all divisors which divides 'num'
    for (int i=2; i<=sqrt(num); i++)
    {
        // if 'i' is divisor of 'num'
        if (num%i==0)
        {
            // if both divisors are same then add
            // it only once else add both
            if (i==(num/i))
                result += i;
            else
                result += (i + num/i);
        }
    }
 
    // Add 1 to the result as 1 is also a divisor
    return (result + 1);
}
```

# Sum of all divisors of all numbers from 1 to n -
![[WhatsApp Image 2024-05-02 at 17.30.20_362ec5a5.jpg]]
```C++
// Utility function to find sum of
// all divisor of number up to 'n'
int divisorSum(int n)
{
	int sum = 0;
	for (int i = 1; i <= n; ++i)
		sum += (n / i) * i;
	return sum;
}

```
