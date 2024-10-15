[Shortest Path to Get All Keys - LeetCode](https://leetcode.com/problems/shortest-path-to-get-all-keys/description/)

The thing is, here we might have to visit one cell multiple times, so the way to do this is to get the keys, and store it in a bitmask fashion so that it represents a number. The number of keys are only 6 so the dimension of the visited array will be at max mxnx(2^6 + 2^5 + 2^4 +....) 
The set bits will make a unique number everytime u try to visit back a cell as u will have different key counts. So u can visit again if need arises
bitmask is also memory and time complexity friendly
So the visited array index is {x, y, keys}

```C++
class Solution {
public:
    int shortestPathAllKeys(vector<string>& grid) {
        //maintain an array of keys of size 6
        //first store the number of keys so that we know when to stop
        int max_len=-1;
        int m=grid.size(), n=grid[0].size();
        int a=-1,b=-1;
        for(int i=0; i<m; i++)
        {
            for(int j=0; j<n; j++)
            {
                if(grid[i][j]>='a' && grid[i][j]<='f') max_len=max(grid[i][j]-'a'+1, max_len);
                if(grid[i][j]=='@') {a=i, b=j;}
            }
        }
        vector<int> start = {0,a,b};
        unordered_set<string> visited;
        visited.insert(to_string(0)+" "+to_string(a)+" "+to_string(b));
        queue<vector<int>> q;
        q.push(start);
        int steps=0;
        vector<vector<int>> dirs = {{0, 1}, {0, -1}, {1, 0}, {-1, 0}};
        while(!q.empty())
        {
            int size=q.size();
            while(size-->0)
            {
                vector<int> curr=q.front();
                q.pop();

                if(curr[0]==(1<<max_len)-1) return steps;
                for(auto d:dirs)
                {
                    int i=curr[1]+d[0];
                    int j=curr[2]+d[1];
                    int keys = curr[0];
                    if(i>=0 && i<m && j>=0 && j<n)
                    {
                        char c=grid[i][j];
                        if(c=='#') continue;
                        if(c>='a' && c<='f') keys|=1<<(c-'a');
                        if(c>='A' && c<='F' && ((keys>> (c-'A')) & 1)==0){
                            continue;
                        }
                        if(!visited.count(to_string(keys)+" "+to_string(i)+" "+to_string(j))){
                            visited.insert(to_string(keys)+" "+to_string(i)+" "+to_string(j));
                            q.push({keys,i,j});
                        }
                    } 
                }
                
            }
            ++steps;
        }
        return -1;
    }
};
```

