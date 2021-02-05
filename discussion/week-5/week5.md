# Discussion Session Week 5
By Licheng Guo and Devyan Biswas

## Goal
- Practice applying recursion to solve problems
- Then solve the same problem without recursion
- Problem 1: inverting a binary tree (3 methods)
- Problem 2: flattening a binary tree (6 methods)
- Never try to memorize the code. Instead, run examples with paper and pencil to feel the idea behind, and then you could naturally write out the code.

## Invert A Binary Tree


Input
```
     A
   /   \
  B     C
 / \   / \
D   E F   G
```

Output
```
     A
   /   \
  C     B
 / \   / \
G   F E   D
```

Solution 1: Doing it recursively:
```c++
TreeNode* invertTree(TreeNode* root) {
  if (root == nullptr) return nullptr;

  swap(root->left, root->right);

  root->left = invertTree(root->left);
  root->right = invertTree(root->right);

  return root;
}
 ```

Follow-up:
- Will this work?
```c++
TreeNode* invertTree(TreeNode* root) {
  if (root == nullptr) return nullptr;

  root->left = invertTree(root->left);
  swap(root->left, root->right);
  root->left = invertTree(root->left);

  return root;
}
```

- Achieve the same goal but without recursion?
 ```c++
TreeNode* traverse(TreeNode* root) {
  if (root == nullptr) return nullptr;

  printf("%d\n",root->val);

  root->left = traverse(root->left);
  root->right = traverse(root->right);

  return root;
}
 ```

```
    1
   / \
  2   5
 / \   \
3   4   6
```

Solution:
```c++
0  void traverse(TreeNode *root) {
1    stack<TreeNode*> s;
2    TreeNode *curr = root;
3  
4    while (curr || !s.empty() ) {
5      if (curr) {
?        printf("%d\n",curr->val);
6        s.push(curr);
7        curr = curr->left;
8      }
9      else {
10       curr = s.top(); s.pop();
11       curr = curr->right;
12     }
13   }

}
```
Follow-up:
- Where should the printf statement go?

- Suppose the reference is like this, where should the printf statement go?

```
    A   
   / \
  B   C
 / \   \
D   E   F

    4   
   / \
  2   5
 / \   \
1   3   6
```
 ```c++
TreeNode* traverse(TreeNode* root) {
  if (root == nullptr) return nullptr;

  root->left = traverse(root->left);
  printf("%d\n",root->val);
  root->right = traverse(root->right);

  return root;
}
 ```

```c++
0  void traverse(TreeNode *root) {
1    stack<TreeNode*> s;
2    TreeNode *curr = root;
3  
4    while (curr || !s.empty() ) {
5      if (curr) {
6        s.push(curr);
7        curr = curr->left;
8      }
9      else {
10       curr = s.top(); 
         printf("%d\n",curr->val);
         s.pop();
11       curr = curr->right;
12     }
13   }

}
```

- What about now? => Actually impossible! Because we will skip the node when we need to print its value.

 ```c++
TreeNode* traverse(TreeNode* root) {
  if (root == nullptr) return nullptr;

  root->left = traverse(root->left);
  root->right = traverse(root->right);
  printf("%d\n",root->val);

  return root;
}
 ```

- Can we make some slight modification to our iterative approach to produce the post-traversal result?

 ```c++
vector<int> ans;

TreeNode* traverse(TreeNode* root) {
  if (root == nullptr) return nullptr;

  root->left = traverse(root->left);
  root->right = traverse(root->right);
  ans.push_back(root->val);
 
  return root;
}
```

The following recusive method achieves the same goal:
```c++
vector<int> ans;

TreeNode* traverse(TreeNode* root) {
  if (root == nullptr) return nullptr;

  ans.push_back(root->val);
  root->right = traverse(root->right);
  root->left = traverse(root->left);

  return root;
}
```

Doing it in a non-recursive way:
```c++
0  void traverse(TreeNode *root) {
1    stack<TreeNode*> s;
2    TreeNode *curr = root;
3    vector<int> ans;

4    while (curr || !s.empty() ) {
5      if (curr) {
         ans.push_back(root->val);
6        s.push(curr);
7        curr = curr->right;
8      }
9      else {
10       curr = s.top(); s.pop();
11       curr = curr->left;
12     }
13   }
    reverse(ans);
}
```