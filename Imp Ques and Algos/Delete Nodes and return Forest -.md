# Done
```C++
class Solution {
public:
    unordered_map<int, int> del;
    TreeNode* remove(TreeNode* root, vector<TreeNode*>& forest){
        if(root == NULL) return NULL;

        root->left = remove(root->left, forest);
        root->right = remove(root->right, forest);

        if(del.find(root->val)!=del.end()) 
        {
            if(root->left!=NULL)
            {
                forest.push_back(root->left);
            }
            if(root->right!=NULL)
            {
                forest.push_back(root->right);
            }
            return NULL;
        }
        return root;
    }
    vector<TreeNode*> delNodes(TreeNode* root, vector<int>& to_delete) {
        vector<TreeNode*> forest;
        for(int i=0; i<to_delete.size(); i++)
        {
            del[to_delete[i]]++;
        }

        remove(root, forest);
        if(del.find(root->val)==del.end())
        {
            forest.push_back(root);
        }
        return forest;
    }
};
```

