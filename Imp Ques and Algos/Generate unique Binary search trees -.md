With values from 1 to A.
```C++
vector<TreeNode*> solve(int s,int e)
{
    vector<TreeNode*> ans;
    if(s>e) return {NULL};
    for(int i=s;i<=e;i++)
    {
        vector<TreeNode*> leftsubtree=solve(s,i-1);
        vector<TreeNode*> rightsubtree=solve(i+1,e);
        for(auto l:leftsubtree){
            for(auto r:rightsubtree){
                TreeNode* newroot=new TreeNode(i);
                newroot->left=l;
                newroot->right=r;
                ans.push_back(newroot);
            }
        }
    }
    return ans;
}
 
vector<TreeNode*> Solution::generateTrees(int A) {
    return solve(1,A);
}
```