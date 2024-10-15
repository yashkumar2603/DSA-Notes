# Done
https://leetcode.com/problems/distribute-coins-in-binary-tree/description/?envType=daily-question&envId=2024-05-18

<font color="#f79646">Asked in many many companies, mostly all imp. MNCs so VERY IMPORTANT</font>
https://www.youtube.com/watch?v=RkVF5PdZJ1w

We will do a recursion, for every node, we require 1 coin. So if a node ha 0 coins, it will ask the parent to give it 1 coin and if the node has more than 1 coin, then it will give the excess to its parent. This way we can distribute. The ask will be -ve sign and the give will be +ve. Also the $number of steps = \sum abs(ask \space or \space give)$  

```C++
int steps = 0;
int dfs(TreeNode* node){
	if(node == nullptr) return 0; //base case
	int leftRequired = dfs(node->left);
	int rightRequired = dfs(node->right);
	steps += abs(leftRequired)+abs(rightRequired);
	return (node->val - 1) + leftRequired + rightRequired;
}

int distributeCoins(TreeNode* root){
	dfs(root);
	return steps;
}
```

