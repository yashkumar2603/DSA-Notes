` left < root < right `

# Create BST-
```C++
struct node {
	int key;
	struct node *left, *right;
};

// A utility function to create a new BST node
struct node* newNode(int item)
{
	struct node* temp
		= new struct node;
	temp->key = item;
	temp->left = temp->right = NULL;
	return temp;
}
```
# Search in BST-
```C++
// Utility function to search a key in a BST
struct node* search(struct node* root, int key)
{
	// Base Cases: root is null or key is present at root
	if (root == NULL || root->key == key)
		return root;

	// Key is greater than root's key
	if (root->key < key)
		return search(root->right, key);

	// Key is smaller than root's key
	return search(root->left, key);
}
```

# Insert in BST - 
```C++
// A utility function to insert a new node with given key in BST
struct node* insert(struct node* node, int key)
{
	// If the tree is empty, return a new node
	if (node == NULL)
		return newNode(key);

	// Otherwise, recur down the tree
	if (key < node->key)
		node->left = insert(node->left, key);
	else if (key > node->key)
		node->right = insert(node->right, key);

	// Return the (unchanged) node pointer
	return node;
}
```

# Print all elements in given range - 

```C++
public void findRange( Node node, int k1, int k2 ){
  if( node == null || (k1>k2) ){
    return;
  }
  int data = node.getData();
  if( data >= k1 && data <= k2 ){
    System.out.println(data);
  }
  if( k1 < data ){
    findRange( node.getLeft(), k1, k2 );
  }
  if( k2 > data ){
    findRange( node.getRight(), k1, k2 );
  }
}
```

# Return the path from root to node as a vector - 
```C++
vector<int>* getRootToNodePath(BinaryTreeNode<int>* root, int data) {

    if (root == NULL) {
        return NULL;
    }
    
    if (root->data == data) {
        vector<int>* output = new vector<int>();
        output->push_back(root->data);
        return output;
    }
    
    vector<int>* leftOutput = getRootToNodePath(root->left, data);
    if (leftOutput != NULL) {
        leftOutput->push_back(root->data);
        return leftOutput;
    }
  
    vector<int>* rightOutput = getRootToNodePath(root->right, data);
    if (rightOutput != NULL) {
            rightOutput->push_back(root->data);
            return rightOutput;
    } else {
        return NULL;
    }
}
```
