# Tree
+ [Binary Tree Inorder Traversal](#binary-tree-inorder-traversal)
+ [Symmetric Tree](#symmetric-tree)

Definition for a binary tree node.
```C++
struct TreeNode {
    int val;
    TreeNode *left;
    TreeNode *right;
    TreeNode(int x) : val(x), left(NULL), right(NULL) {}
};
 ```

## Binary Tree Inorder Traversal
https://leetcode.com/problems/binary-tree-inorder-traversal/

recursively
```C++
class Solution {
public:
    void reqursionTraversal (TreeNode* root, vector<int>& inorder) {
        if (root){
            reqursionTraversal(root->left, inorder);
            inorder.push_back(root->val);
            reqursionTraversal(root->right, inorder);
        }
    }
    vector<int> inorderTraversal(TreeNode* root) {
        vector<int> result(0);
        reqursionTraversal(root, result);
        return result;
    }
};
```
iteratively
```C++
class Solution {
public:
    vector<int> inorderTraversal(TreeNode* root) {
        vector<int> result;
        stack<TreeNode*> treeHigh;
        TreeNode* currentNode = root;
        while (currentNode || !treeHigh.empty()){
            while (currentNode) {
                treeHigh.push(currentNode);
                currentNode = currentNode->left;
            }
            currentNode = treeHigh.top();
            treeHigh.pop();
            result.push_back(currentNode->val);
            currentNode = currentNode->right;
        }
        return result;
    }
};
```
## Symmetric Tree
https://leetcode.com/problems/symmetric-tree/

reqursively
```C++
class Solution {
public:
    bool reqursionMirror(TreeNode* tree1, TreeNode* tree2) {
        if (!tree1 && !tree2)
            return true;
        else if (!tree1 || !tree2)
            return false;
        return (tree1->val == tree2->val) 
            && reqursionMirror(tree1->left, tree2->right) /*   /\    */
            && reqursionMirror(tree1->right, tree2->left); /*  \/    */
    }
    bool isSymmetric(TreeNode* root) {
        return reqursionMirror(root, root);
    }
};
```

iteratively
```C++
class Solution {
public:
    bool isSymmetric(TreeNode* root) {
        if (!root)
            return true;
        stack <TreeNode*>  left, right;
        left.push(root->left);
        right.push(root->right);
        TreeNode *curR, *curL;
        while(1) {
            ......
        }
    }
};
```

```C++
```

```C++
```
