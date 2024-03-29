# Linked Lists
+ [Reorder List](#reorder-list)
+ [Linked List Cycle II](#linked-list-cycle-ii)
+ [Linked List Cycle](#linked-list-cycle)
+ [Merge Two Sorted Lists](#merge-two-sorted-lists)
+ [Remove Nth Node From End of List](#remove-nth-node-from-end-of-list)
+ [Middle of the Linked List](#middle-of-the-linked-list)
+ [Delete Node in a Linked List](#delete-node-in-a-linked-list)
+ [Palindrome Linked List](#palindrome-linked-list)
+ [Reverse Linked List](#reverse-linked-list)
+ [Remove Linked List Elements](#remove-linked-list-elements)
+ [Intersection of Two Linked Lists](#intersection-of-two-linked-lists)
+ [Merge Sort List](#merge-sort-list)

##  Reorder List
https://leetcode.com/problems/reorder-list/

```C++
class Solution {
public:
    ListNode* reverseList(ListNode* head){
        if (!head || !head->next)
            return head;
        ListNode* prev = NULL;
        ListNode* help = head;
        while (help){
            head = help;
            help = head->next;
            head->next = prev;
            prev = head;
        }
        return head;
    }
    
    ListNode* middleNode(ListNode* head) {
        ListNode* fastPtr = head;
        ListNode* slowPtr = head;
        while (fastPtr && fastPtr->next && fastPtr->next->next) {
            fastPtr = fastPtr->next->next;
            slowPtr = slowPtr->next;
        }
        return slowPtr;
    }
    
    
    void reorderList(ListNode* head) {
        if (!head || !head->next || !head->next->next)
            return;
        
        ListNode* tmp = middleNode(head);
        ListNode* second = tmp->next;
        ListNode* help;
        tmp->next = NULL;
        second = reverseList(second);
        
        tmp = head;
        while (tmp && second){
            help = tmp->next;
            tmp->next = second;
            second = second->next;
            tmp->next->next = help;
            tmp = help;
        }
    }
};
```

## Linked List Cycle II
https://leetcode.com/problems/linked-list-cycle-ii/

```C++
class Solution {
public:
     ListNode * hasCycle(ListNode *head) {
        ListNode* slowPtr = head;
        ListNode* fastPtr = head;
        if (!head || !head->next)
            return NULL;
        while (fastPtr->next && fastPtr->next->next){
            fastPtr = fastPtr->next->next;
            slowPtr = slowPtr->next;
            if (fastPtr->next == slowPtr->next)
                return fastPtr;
        }
        return NULL;
    }
    ListNode *detectCycle(ListNode *head) {
        if (!head)
            return NULL;
        ListNode* headTmp = head;
        ListNode* meetNode = hasCycle(head);
        if (!meet)
            return NULL;
        while (headTmp != meet){
            meetNode = meetNode->next;
            headTmp = headTmp->next;
        }
        return headTmp;
    }
};
```

## Linked List Cycle
https://leetcode.com/problems/linked-list-cycle/

```C++
class Solution {
public:
    bool hasCycle(ListNode *head) {
        if (!head || !head->next)
            return false;       
        ListNode* slowPtr = head;
        ListNode* fastPtr = head;
        while (fastPtr->next && fastPtr->next->next){
            fastPtr = fastPtr->next->next;
            slowPtr = slowPtr->next;
            if (fastPtr->next == slowPtr->next)
                return true;
        }
        return false;
    }
};
```

## Merge Two Sorted Lists
https://leetcode.com/problems/merge-two-sorted-lists/

```C++
class Solution {
public:
    ListNode* mergeTwoLists(ListNode* l1, ListNode* l2) {
        ListNode* head = new ListNode(0);
        ListNode* tmp = head;
        while (l1 && l2){
            if (l1->val > l2->val){
                tmp->next = l2;
                l2 = l2->next;
            }
            else{
                tmp->next = l1;
                l1 = l1->next;
            }
            tmp = tmp->next;
        }
        tmp->next = l1? l1 : l2;
        tmp = head;
        head = head->next;
        delete(tmp);
        return head;
    }
};
```

## Remove Nth Node From End of List
https://leetcode.com/problems/remove-nth-node-from-end-of-list/

```C++
class Solution {
public:
    ListNode* removeNthFromEnd(ListNode* head, int n) {
        ListNode* N = head;
        ListNode* buf;
        ListNode* tmp = head;
        for (unsigned i = 0; i < (n - 1); i++){
            tmp = tmp->next;
        }
        ListNode* prev = NULL;
        while(tmp->next){
            prev = N;
            N = N->next;
            tmp = tmp->next;
        }
        if (N == head){
            buf = head->next;
            delete(head);
            return buf;
        }
        buf = prev->next;
        prev->next  = prev->next->next;
        delete(buf);
        return head;
    }
};
```

## Middle of the Linked List
https://leetcode.com/problems/middle-of-the-linked-list/

Time Complexity: O(n)
Space Complexity: O(1)

Slow
```C++
class Solution {
public:
    ListNode* middleNode(ListNode* head) {
        unsigned size = 0;
        ListNode* tmp = head;
        for(size; tmp!= NULL; size++) {
            tmp = tmp->next;
        }
        unsigned half = size / 2;
        tmp = head;
        for (unsigned i = 0; i < half; i++){
            tmp = tmp->next;
        }
        return tmp;
    }
};
```
Faster
```C++
class Solution {
public:
    ListNode* middleNode(ListNode* head) {
        ListNode* fastPtr = head;
        ListNode* slowPtr = head;
        while (fastPtr && fastPtr->next) {
            fastPtr = fastPtr->next->next;
            slowPtr = slowPtr->next;
        }
        return slowPtr;
    }
};
```

## Delete Node in a Linked List
https://leetcode.com/problems/delete-node-in-a-linked-list/

Really strange way
```C++
class Solution {
public:
    void deleteNode(ListNode* node) {
        while(node->next->next) {
            node->val = node->next->val;
            node = node->next;
        }
        node->val = node->next->val;
        delete(node->next);
        node->next = NULL;
    }
};
```

Normal
```C++
class Solution {
public:
    void deleteNode(ListNode* node) {
        ListNode* del = node->next;
        node->val = node->next->val;
        node->next = node->next->next;
        delete(del);
    }
};
```

## Palindrome Linked List
https://leetcode.com/problems/palindrome-linked-list/

```C++
class Solution {
public:
    ListNode* reverseList(ListNode* head){
        if (!head || !head->next)
            return head;
        ListNode* prev = NULL;
        ListNode* help = head;
        while (help){
            head = help;
            help = head->next;
            head->next = prev;
            prev = head;
        }
        return head;
    }
    
    ListNode* middleNode(ListNode* head) {
        ListNode* fastPtr = head;
        ListNode* slowPtr = head;
        while (fastPtr && fastPtr->next && fastPtr->next->next) {
            fastPtr = fastPtr->next->next;
            slowPtr = slowPtr->next;
        }
        return slowPtr;
    }
    
    bool isPalindrome(ListNode* head) {
        if (!head || !head->next)
            return true;
        ListNode* tmp = middleNode(head);
        ListNode* second = tmp->next;
        tmp->next = NULL;
        second = reverseList(second);
        tmp = head;
        while (tmp && second){
            if (tmp->val != second->val)
                return false;
            tmp = tmp->next;
            second = second->next;
        }
        return true;
    }
};
```

## Reverse Linked List
https://leetcode.com/problems/reverse-linked-list/

Recursively
```C++
class Solution {
public:
    ListNode* reverseList(ListNode* head) {
        if (!head || !head->next){
            return head;
        }
        if (!head->next->next){
            ListNode* help = head;
            head = head->next;
            head->next = help;
            head->next->next = NULL;
            return head;
        }
        Solution rez;
        ListNode* tmp = rez.reverseList(head->next);
        ListNode* rememberHead = head;
        head = tmp;
        ListNode* help = head;
        while (help->next)
            help = help->next;
        help->next = rememberHead;
        help->next->next = NULL;
        return head;
    }
}
```

iteratively
```C++
class Solution {
public:
        if (!head || !head->next)
            return head;
        ListNode* prev = NULL;
        ListNode* help = head;
        while (help){
            head = help;
            help = head->next;
            head->next = prev;
            prev = head;
        }
        return head;
    }
};
```

## Remove Linked List Elements
https://leetcode.com/problems/remove-linked-list-elements/

```C++
class Solution {
public:
    ListNode* removeElements(ListNode* head, int val) {
        ListNode* tmp;
        ListNode* pretmp;
        while (head && head->val == val){
            tmp = head;
            head = head->next;
            delete(tmp);
        }
        if (!head)
            return NULL;
        pretmp = head;
        tmp = head->next;
        while (tmp) {
            if (tmp->val == val) {
                pretmp->next = tmp->next;
                delete(tmp);
                tmp = pretmp->next;
                continue;
            }
            pretmp = tmp;
            tmp = tmp->next;
        }
        return head;
    }
};
```

## Intersection of Two Linked Lists
https://leetcode.com/problems/intersection-of-two-linked-lists/

Approach "Two Pointers"
```C++
class Solution {
public:
    ListNode *getIntersectionNode(ListNode *headA, ListNode *headB) {
        ListNode *tmpA = headA, *tmpB = headB;
        while(tmpA && tmpB){
            if(tmpB == tmpA)
                return tmpB;
            tmpA = tmpA->next;
            tmpB = tmpB->next;
            if(!tmpA)
                tmpA = headB;
            else if(!tmpB)
                tmpB = headA;
        }
        return NULL;
    }
};
```

## Merge Sort List
https://leetcode.com/problems/sort-list/submissions/

```C++
class Solution {
public:
    ListNode* mergeTwoLists(ListNode* l1, ListNode* l2) {
        ListNode* head = new ListNode(0);
        ListNode* tmp = head;
        while (l1 && l2){
            if (l1->val > l2->val){
                tmp->next = l2;
                l2 = l2->next;
            }
            else{
                tmp->next = l1;
                l1 = l1->next;
            }
            tmp = tmp->next;
        }
        tmp->next = l1? l1 : l2;
        tmp = head;
        head = head->next;
        delete(tmp);
        return head;
    }
    ListNode* cutMiddle(ListNode* head) {
        ListNode* fast = head;
        ListNode* slow = head;
        while (fast && fast->next && fast->next->next) {
            fast = fast->next->next;
            slow = slow->next;
        }
        ListNode* middle = slow->next;
        slow->next = NULL;
        return middle;
    }
    ListNode* sortList(ListNode* head) {
        if(!head || !head->next)
            return head;
        return mergeTwoLists(sortList(head),sortList(cutMiddle(head)));
    }
};
```
