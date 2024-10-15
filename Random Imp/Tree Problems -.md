#### Striver

**Level Order Traversal -** 
https://leetcode.com/problems/binary-tree-level-order-traversal/description/
```C++
class Solution {
public:
    vector<vector<int>> levelOrder(TreeNode* root) {
        //BFS -> use Queue
        queue<TreeNode*> q;
        vector<vector<int>> ans;
        if(!root) return {};
        q.push(root);
        while(!q.empty())
        {
            int s=q.size();
            vector<int> tmp;
            for(int i=0; i<s; i++)
            {
                auto curr = q.front();
                q.pop();
                if(curr) {
                    tmp.push_back(curr->val);
                    if(curr->left) q.push(curr->left);
                    if(curr->right) q.push(curr->right);
                }
            }
            ans.push_back(tmp);
        }
        return ans;
    }
};
```

**Find the Maximum depth(max-height) of the Binary tree -** 
https://leetcode.com/problems/maximum-depth-of-binary-tree/
A binary tree's **maximum depth** is the number of nodes along the longest path from the root node down to the farthest leaf node.
```C++
class Solution {
public:
    void solve(TreeNode* root, int len,int &maxlen){
        if(root==NULL){
            return;
        }else if(root->left==NULL && root->right==NULL){
            maxlen=max(len, maxlen);  //reached leaf 
            //so this is the final depth
        }
        solve(root->left,len+1,maxlen);
        solve(root->right,len+1,maxlen);
    }
    int maxDepth(TreeNode* root) {
        /*For Root Node declare len as 1*/
        int len=1;
        int maxlen=0;
        solve(root,len,maxlen);
        return maxlen;
    }
};
```

**Check if the Tree is height balanced or not**
If the difference between heights of the left and right halves is <= 1, then it is balanced. 
```C++
class Solution {
public:
    int check(TreeNode* node) { // find height in O(N)
        if (node == NULL)
            return 0;
        int lh = check(node->left);
        int rh = check(node->right);
        if (lh == -1 || rh == -1)  //if any side has an unbalance, whole tree is considered unbalanced
            return -1;
        if (abs(lh - rh) > 1)
            return -1;
        return max(lh, rh) + 1; //return max height if balanced.
    }
    bool isBalanced(TreeNode* root) {
        if(check(root)==-1) return false;
        return true;
    }
};
```
The check function returns -1 if the tree is unbalanced, the max height otherwise.

**Diameter in O(N) -** 
https://leetcode.com/problems/diameter-of-binary-tree/description/
```C++
class Solution {
public:
    int check(TreeNode* node, int& maxi) { 
        if (node == NULL)
            return 0;
        int lh = check(node->left, maxi);
        int rh = check(node->right, maxi);
        maxi=max(maxi, lh+rh);
        return 1+max(lh, rh);
    }
    int diameterOfBinaryTree(TreeNode* root) {
        int maxi=0;
        check(root, maxi);
        return maxi;
    }
};
```

**Maximum path sum in binary tree -**
https://leetcode.com/problems/binary-tree-maximum-path-sum/
```C++
class Solution {
public:
    int check(TreeNode* node, int& ans, int& su) { 
        if (node == NULL)
            return 0;
        int lh = max(0,check(node->left, ans, su));
        int rh = max(0,check(node->right, ans, su));
        su = node->val + max(lh,rh);
        ans=max(ans, node->val + lh+ rh);
        return su;
    }
    int maxPathSum(TreeNode* root) {
        int ans=INT_MIN;
        int su=0;
        check(root, ans, su);
        return ans;
    }
};
```

**Boundary traversal -** (leetcode Premium problem)
https://www.youtube.com/watch?v=0ca1nvR0be4

**Vertical Order Traversal(hard) -**
https://leetcode.com/problems/vertical-order-traversal-of-a-binary-tree/description/
![[Pasted image 20240710205543.png]]
![[Pasted image 20240710220811.png]]
make a queue having (node, vertical, level) + map<int, map<int, multiset< int>> it maps every vertical number to a level map, having multiple nodes and we are using multiset because we wan overlapping nodes to be in sorted order and they might also have same values, so we cant take set.
```C++
vector<vector<int>> verticalTraversal(TreeNode* root){
        // Map to store nodes based on
        // vertical and level information
        map<int, map<int, multiset<int>>> nodes;
        // Queue for BFS traversal, each
        // element is a pair containing node
        // and its vertical and level information
        queue<pair<TreeNode*, pair<int, int>>> todo;
        // Push the root node with initial vertical
        // and level values (0, 0)
        todo.push({root, {0, 0}});
        // BFS traversal
        while(!todo.empty()){
            // Retrieve the node and its vertical
            // and level information from
            // the front of the queue
            auto p = todo.front();
            todo.pop();
            TreeNode* temp = p.first;
            // Extract the vertical and level information
            // x -> vertical
            int x = p.second.first;  
            // y -> level
            int y = p.second.second;
            // Insert the node value into the
            // corresponding vertical and level
            // in the map
            nodes[x][y].insert(temp->val);
            // Process left child
            if(temp->left){
                todo.push({
                    temp->left,
                    {
                        // Move left in
                        // terms of vertical
                        x-1, 
                        // Move down in
                        // terms of level
                        y+1  
                    }
                });
            }
            // Process right child
            if(temp->right){
                todo.push({
                    temp->right, 
                    {
                        // Move right in
                        // terms of vertical
                        x+1, 
                        // Move down in
                        // terms of level
                        y+1  
                    }
                });
            }
        }
        // Prepare the final result vector
        // by combining values from the map
        vector<vector<int>> ans;
        for(auto p: nodes){
            vector<int> col;
            for(auto q: p.second){
                // Insert node values
                // into the column vector
                col.insert(col.end(), q.second.begin(), q.second.end());
            }
            // Add the column vector
            // to the final result
            ans.push_back(col);
        }
        return ans;
    }
```

**Lowest Common Ancestor -** 
https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-tree/
```C++
class Solution {
public:
    TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
        if(!root) return NULL;
        if(root == p) return p;
        if(root==q) return q;
        TreeNode* l = lowestCommonAncestor(root->left, p, q);
        TreeNode* r = lowestCommonAncestor(root->right, p, q);

        if(l==NULL && r==NULL) return NULL;
        else if(l!=NULL && r!=NULL) return root;
        else if(l==NULL) return r;
        else return l;
    }
};
```

**Construct Binary tree from Preorder and In-order -** 
https://leetcode.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal/description
![[Pasted image 20240711132800.png]]

```C++
class Solution {
public:
    // Function to build a binary tree
    // from preorder and inorder traversals
    TreeNode* buildTree(vector<int>& preorder, vector<int>& inorder){
        // Create a map to store indices
        // of elements in the inorder traversal
        map<int, int> inMap;
        
        // Populate the map with indices
        // of elements in the inorder traversal
        for(int i = 0; i < inorder.size(); i++){
            inMap[inorder[i]] = i;
        }
        
        // Call the private helper function
        // to recursively build the tree
        TreeNode* root = buildTree(preorder, 0, preorder.size()-1, inorder, 0, inorder.size()-1, inMap);
        
        return root;
    }

private:
    // Recursive helper function to build the tree
    TreeNode* buildTree(vector<int>& preorder, int preStart, int preEnd, 
            vector<int>& inorder, int inStart, int inEnd, map<int, int>& inMap){
                // Base case: If the start indices 
                // exceed the end indices, return NULL
                if(preStart > preEnd || inStart > inEnd){
                    return NULL;
                }
                
                // Create a new TreeNode with value
                // at the current preorder index
                TreeNode* root = new TreeNode(preorder[preStart]);
                
                // Find the index of the current root
                // value in the inorder traversal
                int inRoot = inMap[root->val];
                
                // Calculate the number of
                // elements in the left subtree
                int numsLeft = inRoot - inStart;
                
                // Recursively build the left subtree
                root->left = buildTree(preorder, preStart + 1, preStart + numsLeft, 
                                inorder, inStart, inRoot - 1, inMap);
                
                // Recursively build the right subtree
                root->right = buildTree(preorder, preStart + numsLeft + 1, preEnd, 
                                inorder, inRoot + 1, inEnd, inMap);
                
                // Return the current root node
                return root;
            }
};
```

**Construct binary tree form inorder and post-order traversal -** 
https://leetcode.com/problems/construct-binary-tree-from-inorder-and-postorder-traversal/description/
```C++
class Solution {
public:
    // Function to build a binary tree
    // from inorder and postorder traversals
    TreeNode* buildTree(vector<int>& inorder, vector<int>& postorder) {
        if (inorder.size() != postorder.size()) {
            return NULL;
        }

        // Create a map to store the indices
        // of elements in the inorder traversal
        map<int, int> hm;
        for (int i = 0; i < inorder.size(); i++) {
            hm[inorder[i]] = i;
        }

        // Call the recursive function
        // to build the binary tree
        return buildTreePostIn(inorder, 0, inorder.size() - 1, postorder, 0,
            postorder.size() - 1, hm);
    }

    // Recursive function to build a binary
    // tree from inorder and postorder traversals
    TreeNode* buildTreePostIn(vector<int>& inorder, int is, int ie,
        vector<int>& postorder, int ps, int pe, map<int, int>& hm) {

        // Base case: If the subtree
        // is empty, return NULL
        if (ps > pe || is > ie) {
            return NULL;
        }

        // Create a new TreeNode
        // with the root value from postorder
        TreeNode* root = new TreeNode(postorder[pe]);

        // Find the index of the root
        // value in inorder traversal
        int inRoot = hm[postorder[pe]];
        
        // Number of nodes in the left subtree
        int numsLeft = inRoot - is; 

        // Recursively build the
        // left and right subtrees
        root->left = buildTreePostIn(inorder, is, inRoot - 1, postorder,
            ps, ps + numsLeft - 1, hm);

        root->right = buildTreePostIn(inorder, inRoot + 1, ie, postorder,
            ps + numsLeft, pe - 1, hm);

        // Return the root of
        // the constructed subtree
        return root;
    }
};

```

<font color="#b2a2c7">Theory -</font>
If we are given the in-order, along with any other order, then we can construct a unique binary tree.
in-order is required to know what is on the left and what is on the right of root (at the back or at the front of the pre or post order)

**Insert in BST**
https://leetcode.com/problems/insert-into-a-binary-search-tree/description/
```C++
class Solution {
public:
    TreeNode* insertIntoBST(TreeNode* root, int val) {
        if (!root)
            return new TreeNode(val);
        TreeNode* curr = root;
        while (true) {
            if (curr->val <= val) {
                if (curr->right)
                    curr = curr->right;
                else {
                    curr->right = new TreeNode(val);
                    break;
                }
            }
            if (curr->val >= val) {
                if (curr->left)
                    curr = curr->left;
                else {
                    curr->left = new TreeNode(val);
                    break;
                }
            }
        }
        return root;
    }
};
```

**Delete a Node in a binary search tree -** 
https://leetcode.com/problems/delete-node-in-a-bst/description/
The rearrangement after deletion makes it difficult
search the node and then delete it, now, the thing is that if we delete it, we can take the right portion and attach it to the rightmost node of the left portion and attach the left portion directly to the previous root.
```C++
TreeNode* deleteNode(TreeNode* root, int key){
	if(root==NULL) return NULL;
	if(root->val==key) return helper(root);

	TreeNode* dummy = root;
	while(root!=NULL){
		if(root->val > key){
			if(root->left!=NULL && root->left->val == key){
				root->left = helper(root->left);
				break;
			}
			else{
				root=root->left;
			}
		}
		else{
			if(root->right!=NULL && root->right->val == key){
				root->right = helper(root->right);
				break;
			}
			else{
				root=root->right;
			}
		}
	}
	return dummy;
}
TreeNode* helper(TreeNode* root){
	if(root->left ==NULL) return root->right;
	if(root->right ==NULL) return root->left;

	TreeNode* rightChild = root->right;
	TreeNode* lastRight = findLastRight(root->left);
	lastRight->right = rightChild;
	return root->left;
}
TreeNode* findLastRight(TreeNode* root){
	if(root->right == NULL) return root;
	return findLastRight(root->right);
}
```

**Lowest Common Ancestor in Binary search tree -**
https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-search-tree/description/
We continue to move until its the same path for both the nodes, the moment the path splits up it is the LCA, or if we hit one of the two nodes that is the LCA itself.
```C++
TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q){
	if(root==NULL) return NULL;
	int curr = root->val;
	if(curr<p->val && curr<q->val) return lowestCommonAncestor(root->right, p,  q);
	if(curr>p->val && curr>q->val) return lowestCommonAncestor(root->left, p, q);
	return root;
}
```

**Construct BST from Preorder -** 
https://leetcode.com/problems/construct-binary-search-tree-from-preorder-traversal/description/
if we try to make it naively, that is take every element and compare and then insert, it takes O(n^2) worst case for skewed tree.
But what we can do is we sort the preorder and get the inorder, then apply the preorder and inorder given code from BT. O(nlogn) now.
Even more efficient is O(n) method

```C++
TreeNode* bstFromPreorder(vector<int>& A){
	int i=0;
	return build(A, i, INT_MAX);
}
TreeNode* build(vector<int>& A, int& i, int bound){
	if(i==A.size() || A[i]>bound) return NULL;
	TreeNode* root = new TreeNode(A[i++]);
	root->left = build(A, i, root->val);
	root->right = build(A, i, bound);
	return root;
}
```

**Inorder Successor in O(1) space -** 
Find the next element in the inorder for the given k.
Brute way of storing inorder and then searching will take O(n) space.
So we improvise by making a inorder on the BST and then the first element that we encounter greater than k, that is the answer.
```C++
TreeNode* inorderSuccessor(TreeNode* root, TreeNode* p){
	treeNode* successor = NULL;
	while(root!=NULL){
		if(p->val >= root->val){
			root=root->right;
		}
		else{
			successor = root;
			root = root->left;
		}
	}
	return successor;
}
```

**If predecessor is asked -** 
Intuition for predecessor: 
-Basically if root.val >= p.val then just go left because predecessor should ideally be on the left so we do not even have a potential predecessor to set at this point because it has to be smaller than the p's val. 
-On the other hand, if root.val < p.val, then we can have a potential predecessor(may or may not be immediate) so we store root.val into predecessor and move right to find a larger value than current predecessor but less than p's val (basically closer value to p but should be less than p of course). 
-In the end when we reach null, we will have predecessor which we will return.
```Python
def inorderPredecessor(self, root, p):
    predecessor = None
    while root:
        if root.val >= p.val:
            root = root.left
       else:
           predecessor = root
           root = root.right
    return predecessor
```


#### NeetCode - 
**Count Good Nodes in a binary tree -**  (Microsoft most asked)
https://leetcode.com/problems/count-good-nodes-in-binary-tree/
```C++
class Solution {
public:
    int func(TreeNode* root, int ma){
        if (!root) return 0;
        int ans = 0;
        if (root->val >= ma) ans = 1;
        ma = max(ma, root->val);
        ans += func(root->left, ma);
        ans += func(root->right, ma);
        return ans;
    }
    int goodNodes(TreeNode* root) {
        //DFS and store path max, if path max>x, dont add
        if(!root) return 0;
        return func(root, root->val);
    }
};
```

Is valid BST - 
```C++
class Solution {
public:
    bool isValidBST(TreeNode* root) {
        return valid(root, LONG_MIN, LONG_MAX);
    }
private:
    bool valid(TreeNode* node, long left, long right) {  //left and right are left and right boundaries for the checking
        if (!node) {
            return true;
        }
        if (!(left < node->val && node->val < right)) {
            return false;
        }

        return valid(node->left, left, node->val) && valid(node->right, node->val, right);
    }
};
```
Edge case - 
![[Pasted image 20240712014037.png]]
if we simply check for neighbors, this gives true but it is a false and to keep the answer correct, we need to pass the correct checking boundaries for it. 

**Kth Smallest Element in BST -** (important and good)
https://leetcode.com/problems/kth-smallest-element-in-a-bst/description/
Inorder is always strictly increasing, so output inorder(k-1) and that is the answer
Now, instead of outputting the inorder(k-1), for which u will need an array to store the inorder, just keep a counter and whe counter == k-1 return  that value and done.
```C++
class Solution {
public:
    void inorder(TreeNode* node, int& counter, int k, int& kSmallest) {
        if (!node || counter >= k) return;
        // Traverse left subtree
        inorder(node->left, counter, k, kSmallest);
        // Increment counter after visiting left subtree
        counter++;
        // Check if current node is the Kth smallest
        if (counter == k) {
            kSmallest = node->val;
            return;
        }
        // Traverse right subtree if
        // Kth smallest is not found yet
        inorder(node->right, counter, k, kSmallest);
    }
    int kthSmallest(TreeNode* root, int k) {
        int ans;
        int count=0;
        inorder(root, count, k,ans);
        return ans;
    }
};
```



