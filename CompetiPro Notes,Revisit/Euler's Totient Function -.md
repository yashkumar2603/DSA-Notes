Euler's totient function, also known as **phi-function**   𝜙(𝑛), counts the number of integers between 1 and   𝑛 inclusive, which are coprime to   𝑛<math xmlns="http://www.w3.org/1998/Math/MathML"><mi>n</mi></math>$n$ . Two numbers are coprime if their greatest common divisor equals   1($1$  is considered to be coprime to any number).

Implementation in $O(\sqrt n)$ 
```C++
int phi(int n) {
    int result = n;
    for (int i = 2; i * i <= n; i++) {
        if (n % i == 0) {
            while (n % i == 0)
                n /= i;
            result -= result / i;
        }
    }
    if (n > 1)
        result -= result / n;
    return result;
}
```

Implementation with sieve - 

If we need all all the totient of all numbers between   1 and   𝑛<math xmlns="http://www.w3.org/1998/Math/MathML"><mi>n</mi></math>$n$ , then factorizing all   𝑛 numbers is not efficient. We can use the same idea as the [Sieve of Eratosthenes](https://cp-algorithms.com/algebra/sieve-of-eratosthenes.html). It is still based on the property shown above, but instead of updating the temporary result for each prime factor for each number, we find all prime numbers and for each one update the temporary results of all numbers that are divisible by that prime number.

Since this approach is basically identical to the Sieve of Eratosthenes, the complexity will also be the same: $O(n \log \log n)$
```C++
void phi_1_to_n(int n) {
    vector<int> phi(n + 1);
    for (int i = 0; i <= n; i++)
        phi[i] = i;

    for (int i = 2; i <= n; i++) {
        if (phi[i] == i) {
            for (int j = i; j <= n; j += i)
                phi[j] -= phi[j] / i;
        }
    }
}
```


