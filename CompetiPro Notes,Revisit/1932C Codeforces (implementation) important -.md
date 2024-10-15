![[Pasted image 20240503142704.png]]
I implemented the brute force method using deque but it didnt work as the product value exceeds the limits of even long long and then starts to give wrong answers. So we have to do something better

>If we perform all deletions except the last one, only one element will remain. Let's find its index in the array. 
>Now we will perform the operations in reverse order, then the deletion operations will become additions, which are much easier to maintain. We will store the remainder of the division of the product of the current segment by m
 and multiply by the new elements when extending the segment. We will output all the obtained numbers in reverse order.

The code for this is - 
```C++
int n, m;
    cin >> n >> m;

    vector<int> a(n);

    for (int i = 0; i < n; i++)
    {
        cin >> a[i];
    }

    string s;
    cin >> s;
    int l = 0, r = n - 1;  

    for (int i = 0; i < n - 1; i++)  //determinin the last remaining element.
    {
        if (s[i] == 'L')
        {
            l++;
        }
        else if (s[i] == 'R')
        {
            r--;
        }
    }
    vector<int> prod(n);
    prod[n - 1] = a[r] % m;  //filling the last element of the answer array with the last answer, i.e. the last remaining element%m
    
    for (int i = n - 2; i >= 0; i--)
    {
	    //filling up the answer array by reproducing the effects in reverse order
        if (s[i] == 'L')
        {
            prod[i] = (prod[i + 1] * a[--l]) % m; //note the use of  --l and ++r here, as we need to reproduce the effect that addition(deleltion in original problem, but addition for our inverted problem) happens from any side of the array.
        }
        else if (s[i] == 'R')
        {
            prod[i] = (prod[i + 1] * a[++r]) % m;
        }
    }
    for (int i = 0; i < n; i++)
    {
        cout << prod[i] << " ";
    }
    cout << nl;
```