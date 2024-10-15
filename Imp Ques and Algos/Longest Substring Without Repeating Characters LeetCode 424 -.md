
<iframe width="560" height="315" src="https://www.youtube.com/embed/-zSxTJkcdAo?si=AeJSQ-tEfmp09MAN" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
Watch this video and see the solution.
# Done
![[Pasted image 20240508143743.png|700]]
<font color="#e36c09">IMPORTANT QUESTION AND IMPORTANT SOLUTION</font>
```C++
int lengthofLongestSubstring(string s) {
      vector < int > mpp(256, -1);

      int left = 0, right = 0;
      int n = s.size();
      int len = 0;
      while (right < n) {
        if (mpp[s[right]] != -1)
          left = max(mpp[s[right]] + 1, left);

        mpp[s[right]] = right;

        len = max(len, right - left + 1);
        right++;
      }
      return len;
    }
```