```C++
// Function to perform modular exponentiation
long long modular_exponentiation(long long base, long long exponent,
                                 long long mod) {
    long long result = 1;
    while (exponent > 0) {
        if (exponent % 2 == 1) {
            result = (result * base) % mod;
        }
        base = (base * base) % mod;
        exponent /= 2;
    }
    return result;
}
```

