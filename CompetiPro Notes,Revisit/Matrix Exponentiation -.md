https://zobayer.blogspot.com/2010/11/matrix-exponentiation.html

To find the $M^k$ which is the major time work - 
```psuedo
function matrix_power_final(A, x):
  result = I_n
  while x > 0:
    if x % 2 == 1:
      result = result * A
    A = A * A
    x = x / 2
  return result
```

![[Pasted image 20240524183200.png]]
