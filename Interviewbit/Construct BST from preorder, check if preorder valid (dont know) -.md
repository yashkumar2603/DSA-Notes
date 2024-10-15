https://www.youtube.com/watch?v=UmJT3j26t1I

https://leetcode.com/problems/construct-binary-search-tree-from-preorder-traversal/description/

```C++
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:

    TreeNode* find(pair<int,int>&p,vector<int>& v,int &i){
        if(i>=v.size() || v[i]>p.second) return NULL;
        TreeNode* root = new TreeNode(v[i]);
        i++;
        int x = p.second;
        p.second = root->val;
        root->left = find(p,v,i);
        p.second = x;
        p.first = root->val;
        root->right = find(p,v,i);
        return root;
    }

    TreeNode* bstFromPreorder(vector<int>& preorder) {
        pair<int,int>p = {INT_MIN,INT_MAX};
        int i=0;
        TreeNode* root = find(p,preorder,i);
        return root;
    }
};
```

