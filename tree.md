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
+ [Inorder Successor in BST](#inorder-successor-in-bst)

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
        while(curR || curL || !stackL.empty()) {
            if (curR && curL) {
                stackL.push(curL);
                stackR.push(curR);
                curL = curL->left;
                curR = curR->right;
            }
            else if (!curR && !curL) {
                curL = stackL.top();
                curR = stackR.top();
                if (curL->val != curR->val)
                    return false;
                curL = curL->right;
                curR = curR->left;
                stackL.pop();
                stackR.pop();
            }
            else 
                return false;
        }
        return true;
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
        swap(root->left, root->right);
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
        if (!(sum - root->val) && !root->left && !root->right)
            return true;
        return hasPathSum(root->left, sum - root->val) 
            || hasPathSum(root->right, sum - root->val);
    }
};
```


## Binary Tree Level Order Traversal
https://leetcode.com/problems/binary-tree-level-order-traversal/

reqursively
```C++
class Solution {
public:
    void createLevels (TreeNode* root, int level, vector<vector<int>>& res) {
        if (!root)
            return;
        if (level >= res.size())
            res.push_back({});
        res[level].push_back(root->val);
        createLevels(root->left, level + 1, res);
        createLevels(root->right, level + 1, res);
    }
    vector<vector<int>> levelOrder(TreeNode* root) {
        vector<vector<int>> res;
        createLevels(root, 0, res);
        return res;
    }
};
```

iteratively
```C++
class Solution {
public:
    vector<vector<int>> levelOrder(TreeNode* root) {
        if (!root)
            return {};
        vector<vector<int>> res;
        queue<TreeNode*> order;
        order.push(root);
        while (order.size()) {
            res.push_back({});
            int sizeLevel = order.size();
            for (int i = 0; i < sizeLevel; ++i) {
                TreeNode* currentNode = order.front();
                order.pop();
                res.back().push_back(currentNode->val);
                if (currentNode->left)
                    order.push(currentNode->left);
                if (currentNode->right)
                    order.push(currentNode->right);
            }
        }
        return res;
    }
};
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
    void inOrder (TreeNode* root, vector<int>& order) {
        if (!root)
            return;
        inOrder (root->left, order);
        order.push_back(root->val);
        inOrder (root->right, order);
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

reqursively
```C++
class Solution {
public:
    TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
        if (!root || !p || !q)
            return NULL;
        if (root->val < p->val && root->val < q->val)
            return lowestCommonAncestor(root->right, p, q);
        else if (root->val > p->val && root->val > q->val)
            return lowestCommonAncestor(root->left, p, q);
        else
            return root;
    }
};
```

iteratively
```C++
class Solution {
public:
    TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
        if (!p || !q)
            return NULL;
        TreeNode* current = root;
        while (current) {
            if (current->val > p->val && current->val > q->val)
                current = current->left;
            else if (current->val < p->val && current->val < q->val)
                current = current->right;
            else 
                return current;
        }
        return NULL;
    }
};
```

## Lowest Common Ancestor of a Binary Tree
https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-tree/

```C++
class Solution {
public:
    TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
        if (!root || root == p || root == q)
            return root;
        TreeNode* L = lowestCommonAncestor(root->left,p,q);
        TreeNode* R = lowestCommonAncestor(root->right,p,q);
        if (root == L || root == R || (R && L))
            return root;
        else return L? L : R;
    }
};
```

## Validate Binary Search Tree
https://leetcode.com/problems/validate-binary-search-tree/

```C++
class Solution {
public:
    // based on iterativetily inorder
    bool isValidBST(TreeNode* root) {
        stack <TreeNode*> treeHigh;
        TreeNode* currentNode = root;
        int prevVal = 0;
        bool isFirst = true;
        while (currentNode || !treeHigh.empty()) {
            while (currentNode) {
                treeHigh.push(currentNode);
                currentNode = currentNode->left;
            }
            currentNode = treeHigh.top();
            treeHigh.pop();
            if (!isFirst && prevVal >= currentNode->val)
                return false;
            prevVal = currentNode->val;
            currentNode = currentNode->right;
            isFirst = false;
        }
        return true;
    }
};
```

## Binary Search Tree Iterator
https://leetcode.com/problems/binary-search-tree-iterator/

Stack approach.
Time complexity - O(1). Though goLeft function is linear (O(N) in the worst case), the amortized (average) time complexity for this function would still be O(1).
Space complexity - O(h)  where h is the height of the tree.
```C++
class BSTIterator {
    stack<TreeNode*> inorderStack;
    void goLeft (TreeNode* root) {
        while (root) {
            inorderStack.push(root);
            root = root->left;
        }
    }
public:
    BSTIterator(TreeNode* root) {
        goLeft(root);
    }
    
    /** @return the next smallest number */
    int next() {
        TreeNode* res = inorderStack.top();
        inorderStack.pop();
        if (res->right)
            goLeft(res->right);
        return res->val;
    }
    
    /** @return whether we have a next smallest number */
    bool hasNext() {
        return !inorderStack.empty();
    }
};
```

## Inorder Successor in BST
Given a binary search tree and a node in it.

```C++
struct TreeNode {
    TreeNode *parent;
    TreeNode *left;
    TreeNode *right;
};
```

Find the in-order successor of that node in the BST.

```C++
TreeNode* inorderSuccessor(TreeNode* node) {
    TreeNode* tmpNode = node;
    TreeNode* tmpParent = node->parent;
    if (tmpParent && tmpParent->left == tmpNode)
        return tmpParent;
    while (tmpParent && tmpParent->right == tmpNode) {
        tmpNode = tmpParent;
        tmpParent = tmpParent->parent;
    }
    if (tmpParent)
        return tmpParent;
    return NULL;
}
```
