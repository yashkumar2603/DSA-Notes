# DP Basic Implementation on Fibbonacci series-

## Top -Down Approach -
```C++

//Recursive Solver(step 1) with memoization (step 3)
int Solve(int n, vector<int> &dp)
{
    if (n == 1 || n == 0)
    {
        return n;
    }
    if (dp[n] != -1)
    {
        return dp[n];
    }
  
    dp[n] = Solve(n - 1, dp) + Solve(n - 2, dp);
    return dp[n];
}

// creating the memoization unit and wrapping up(step 2)
int fib(int n)
{
    vector<int> dp(n + 1, -1);
    int ans = Solve(n, dp);
    return ans;
}

int main()
{
    ios::sync_with_stdio(false);
    cin.tie(nullptr);

    int n;
    cin >> n;
    cout << fib(n);
    
    return 0;
}
```

## Bottom-Up Approach-

```C++
int Solve_BottomUp(int n)
{
    // step1 : Create DP array
    vector<int> dp(n + 1, -1);

    // step 2 : observe base case in recursive solution and try ot clone it in here.
    dp[0] = 0;
    dp[1] = 1;  //Can also check before accessing the 1st element to avoid errors if 0 is asked.

    // step 3: Clone the recursive call
    for (int i = 2; i <= n; i++)
    {
        dp[i] = dp[i - 1] + dp[i - 2];
    }
    return dp[n];
}
```

[Mastering Dynamic Programming - How to solve any interview problem (Part 1) (youtube.com)](https://www.youtube.com/watch?v=Hdr64lKQ3e4)
