[Problem - 1968D - Codeforces](https://codeforces.com/problemset/problem/1968/D)
![[Pasted image 20240601173659.png]]
The Problem involves a greedy strategy, but if we dont reach to the max because of too less number of available turns.
So, the best strategy is to see all paths, after a point the path becomes cyclic, we note down the path in an array(using a visited array to keep track of the visited positions). and then we go on a loop till one of path array or k exhausts. Now, we add the previous score and assume we will spend rest of the turns here only and so $currS = presum + pathb[i-1] * (k-i)$  now score = max of currS and score. 
`"\\wsl.localhost\Ubuntu\home\yamshum\CompiP\D_Permutation_Game.cpp"`
See this file for the full implementation.