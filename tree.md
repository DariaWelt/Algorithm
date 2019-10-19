# Tree
+ [Binary Tree Inorder Traversal](#binary-tree-inorder-traversal)
+ [Symmetric Tree](#symmetric-tree)
+ [Maximum Depth of Binary Tree](#maximum-depth-of-binary-tree)
+ [Same Tree](#same-tree)
+ [Invert Binary Tree](#invert-binary-tree)
+ [Path Sum](#path-sum)
+ [Binary Tree Level Order Traversal](#binary-tree-level-order-traversal)
+ [Subtree of Another Tree](#subtree-of-another-tree)
+ [Kth Smallest Element in a BST](#kth-smallest-element-in-a-bst)
+ [Lowest Common Ancestor of a Binary Search Tree](#lowest-common-ancestor-of-a-binary-search-tree)
+ [Lowest Common Ancestor of a Binary Tree](#lowest-common-ancestor-of-a-binary-tree)
+ [Validate Binary Search Tree](#validate-binary-search-tree)
+ [Binary Search Tree Iterator](#binary-search-tree-iterator)

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
        stack <TreeNode*>  stackL, stackR;
        TreeNode *curR = root->left, *curL = root->right;
        while(1) {
            if (!curR && !curL) {
                if (stackL.empty())
                    return true;
                curL = stackL.top();
                curR = stackR.top();
                if (curL->val != curR->val)
                    return false;
                curL = curL->right;
                curR = curR->left;
                stackL.pop();
                stackR.pop();
            }
            else if (!curR || !curL)
                return false;
            else {
                stackL.push(curL);
                stackR.push(curR);
                curL = curL->left;
                curR = curR->right;
            }
        }
    }
};
```

## Maximum Depth of Binary Tree
https://leetcode.com/problems/maximum-depth-of-binary-tree/submissions/

```C++
class Solution {
public:
    int maxDepth(TreeNode* root) {
        if (!root)
            return 0;
        return max(maxDepth(root->right), maxDepth(root->left)) + 1;
    }
};
```

## Same Tree
https://leetcode.com/problems/same-tree/

```C++
class Solution {
public:
    bool isSameTree(TreeNode* p, TreeNode* q) {
        if (!p && !q){
            return true;
        }
        else if (!p || !q)
            return false;
        else {
           return (p->val == q->val) 
               && isSameTree(p->left, q->left) 
               && isSameTree(p->right, q->right);
        }
    }
};
```

## Invert Binary Tree
https://leetcode.com/problems/invert-binary-tree/submissions/

```C++
class Solution {
public:
    TreeNode* invertTree(TreeNode* root) {
        if (!root)
            return root;
        TreeNode* tmp = root->left;
        root->left = root->right;
        root->right = tmp;
        invertTree(root->left);
        invertTree(root->right);
        return root;
    }
};
```

## Path Sum
https://leetcode.com/problems/path-sum/

```C++
class Solution {
public:
    bool hasPathSum(TreeNode* root, int sum) {
        if(!root)
            return false;
        if (sum - root->val == 0 &&!root->left && !root->right)
            return true;
        return hasPathSum(root->left, sum - root->val) 
            || hasPathSum(root->right, sum - root->val);
    }
};
```


## Binary Tree Level Order Traversal
https://leetcode.com/problems/binary-tree-level-order-traversal/

```C++
```

## Subtree of Another Tree
https://leetcode.com/problems/subtree-of-another-tree/

```C++
class Solution {
public:
    bool isSameTree(TreeNode* p, TreeNode* q) {
        if (!p && !q){
            return true;
        }
        else if (!p || !q)
            return false;
        else {
           return (p->val == q->val) 
               && isSameTree(p->left, q->left) 
               && isSameTree(p->right, q->right);
        }
    }
    bool isSubtree(TreeNode* s, TreeNode* t) {
        if (!s)
            return false;
        return isSameTree(s,t) 
            || isSubtree (s->left, t)
            || isSubtree (s->right, t);
    }
};
```

## Kth Smallest Element in a BST
https://leetcode.com/problems/kth-smallest-element-in-a-bst/

reqursively
```C++
class Solution {
public:
    void inOrder (TreeNode* root, vector<int>& vec) {
        if (!root)
            return;
        inOrder (root->left, vec);
        vec.push_back(root->val);
        inOrder (root->right, vec);
    }
    int kthSmallest(TreeNode* root, int k) {
        vector<int> order;
        inOrder(root, order);
        return order[k - 1];
    }
};
```

##  Lowest Common Ancestor of a Binary Search Tree
https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-search-tree/

```C++
```

## Lowest Common Ancestor of a Binary Tree
https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-tree/

```C++
```

## Validate Binary Search Tree
https://leetcode.com/problems/validate-binary-search-tree/

```C++
```

## Binary Search Tree Iterator
https://leetcode.com/problems/binary-search-tree-iterator/

```C++
```
