# DONE
```C++
class Solution {
public:
    bool isCompleteTree(TreeNode* root) {
        queue<TreeNode*> q;
        q.push(root);
        while(!q.empty())
        {
            TreeNode* node = q.front();
            q.pop();
            if(node){
                q.push(node->left);
                q.push(node->right);
            }
            else{
                while(!q.empty())
                {
                    TreeNode* hehe = q.front();
                    q.pop();
                    if(hehe) return false;
                }
            }
        }
        return true;
    }
};
```

