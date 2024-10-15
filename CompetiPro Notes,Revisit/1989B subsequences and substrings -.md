We are given 2 strings a and b,
return the minimum possible length of the string that contains a𝑎 as a substring and b𝑏 as a subsequence.

So we need to find the max number of common elements in between the 2 strings.
We want the longest subsequence of string a in ur string b. 
answer is then |a|+|b|-common

```C++
int lenX = x.length();
int lenY = y.length();

int maxCommon = 0;
for (int i = 0; i < lenY; i++) {
    int p = i;
    int count = 0;
    for (int j = 0; j < lenX && p < lenY; j++) {
        if (x[j] == y[p]) {
            p++;
            count++;
        }
    }
    maxCommon = max(count, maxCommon);
}

return lenX + lenY - maxCommon;
```

