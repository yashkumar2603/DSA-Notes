# Done
[Balance a Binary Search Tree - LeetCode](https://leetcode.com/problems/balance-a-binary-search-tree/)

We first write the in-order traversal of the tree and store in an array, then we just take the middle element and start balancing, then call once on left side, then once on right side.
```C++
class Solution {
public:
    TreeNode* help2(vector<int> &v, int s, int e)
    {
        if(s>e) return NULL;
        int m=s+(e-s)/2;
        TreeNode* root=new TreeNode(v[m]);
        root->left=help2(v,s,m-1);
        root->right=help2(v,m+1,e);
        return root;
    }
    void help1(TreeNode* root, vector<int> &v)
    {
        if(!root) return;
        help1(root->left,v);
        v.push_back(root->val);
        help1(root->right,v);
    }
    TreeNode* balanceBST(TreeNode* root) {
        vector<int> v;
        help1(root, v);
        return help2(v,0,v.size()-1);
    }
};
```