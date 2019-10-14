# Tree
+ [Binary Tree Inorder Traversal](#binary-tree-inorder-traversal)


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


```C++
```
