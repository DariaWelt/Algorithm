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
    void reorderList(ListNode* head) {
        if (!head || !head->next || !head->next->next)
            return;
        unsigned size = 0;
        ListNode* tmp = head, *help;
        for(size; tmp!= NULL; size++) {
            tmp = tmp->next;
        }
        tmp = head;
        for (unsigned i = 0; i < (size - 1) / 2; i++){
            tmp = tmp->next;
        }
        ListNode* second = tmp->next;
        tmp->next = NULL;
        second = reverseList(second);
        tmp = head;
        while (second && tmp){
            help = tmp->next;
            tmp->next = second;
            second = second->next;
            tmp = tmp->next;
            tmp->next = help;
            tmp = tmp->next;
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
        ListNode* slow = head;
        ListNode* fast = head;
        if (!head || !head->next)
            return NULL;
        while (fast->next && fast->next->next){
            fast = fast->next->next;
            slow = slow->next;
            if (fast->next == slow->next)
                return fast;
        }
        return NULL;
    }
    ListNode *detectCycle(ListNode *head) {
        if (!head)
            return NULL;
        ListNode* headtmp = head;
        ListNode* meet = this->hasCycle(head);
        if (!meet)
            return NULL;
        while (headtmp != meet){
            meet = meet->next;
            headtmp = headtmp->next;
        }
        return headtmp;
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
        ListNode* slow = head;
        ListNode* fast = head;
        while (fast->next && fast->next->next){
            fast = fast->next->next;
            slow = slow->next;
            if (fast->next == slow->next)
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
        if (!l1){
            return l2;
        }
        if(!l2){
            return l1;
        }
        ListNode* head = NULL;
        if (l1->val > l2->val){
            head = l2;
            l2 = l2->next;
        }
        else {
            head = l1;
            l1 = l1->next;
        }
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
        if (l1){
            tmp->next = l1;
            return head;
        }
        else{
            tmp->next = l2;
            return head;
        }
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

Stupid
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
Better
```C++
class Solution {
public:
    ListNode* middleNode(ListNode* head) {
        ListNode* fast = head;
        ListNode* slow = head;
        while (fast && fast->next) {
            fast = fast->next->next;
            slow = slow->next;
        }
        return slow;
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
    void reorderList(ListNode* head) {
        if (!head || !head->next || !head->next->next)
            return;
        unsigned size = 0;
        ListNode* tmp = head, *help;
        for(size; tmp!= NULL; size++) {
            tmp = tmp->next;
        }
        tmp = head;
        for (unsigned i = 0; i < (size - 1) / 2; i++){
            tmp = tmp->next;
        }
        ListNode* second = tmp->next;
        tmp->next = NULL;
        second = reverseList(second);
        tmp = head;
        while (second && tmp){
            help = tmp->next;
            tmp->next = second;
            second = second->next;
            tmp = tmp->next;
            tmp->next = help;
            tmp = tmp->next;
        }
    }
    bool isPalindrome(ListNode* head) {
        if (!head || !head->next)
            return true;
        reorderList(head);
        ListNode* tmp = head;
        while (tmp && tmp->next){
            if (tmp->val != tmp->next->val)
                return false;
            tmp = tmp->next->next;
        }
        return true;
    }
};
```

## Reverse Linked List
https://leetcode.com/problems/reverse-linked-list/

```C++
class Solution {
public:
    ListNode* reverseList(ListNode* head) {
        //Recursively
        /*
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
        */
        
        //iteratively
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

```C++
#include <cmath>
class Solution {
public:
    
    ListNode *getIntersectionNode(ListNode *headA, ListNode *headB) {
        if (headA == NULL || headB == NULL)
          return NULL;
        ListNode* tmp1 = headA;
        ListNode* tmp2 = headB;
        unsigned sizeA = 0, sizeB = 0;
        for (sizeA; tmp1; sizeA++) {
          tmp1 = tmp1->next;
        }
        for (sizeB; tmp2; sizeB++) {
          tmp2 = tmp2->next;
        }
        tmp2 = headB;
        tmp1 = headA;
        if (sizeA > sizeB) {
          for (unsigned i = 0; i < sizeA - sizeB; tmp1 = tmp1->next, ++i) {};
        }
        else if (sizeB > sizeA) {
          for (unsigned i = 0; i < sizeB - sizeA; tmp2 = tmp2->next, ++i);
        }
        while (tmp1 != tmp2 && tmp1 != NULL) {
          tmp1 = tmp1->next;
          tmp2 = tmp2->next;
        }
        if (tmp1 == NULL) {
          return NULL;
        }
        else {
          return tmp1;
        }
    }
};
```

## Merge Sort List
https://leetcode.com/problems/sort-list/submissions/

```C++
class Solution {
public:
    ListNode* mergeTwoLists(ListNode* l1, ListNode* l2) {
        if (!l1){
            return l2;
        }
        if(!l2){
            return l1;
        }
        ListNode* head = NULL;
        if (l1->val > l2->val){
            head = l2;
            l2 = l2->next;
        }
        else {
            head = l1;
            l1 = l1->next;
        }
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
        if (l1){
            tmp->next = l1;
            return head;
        }
        else{
            tmp->next = l2;
            return head;
        }
    }
    ListNode* sortList(ListNode* head) {
        if(!head)
            return NULL;
        if (!head->next)
            return head;
        else {
            ListNode* tmp = head;
            unsigned size = 0;
            for(size; tmp; tmp = tmp->next, ++size);
            tmp = head;
            for(unsigned i = 0; i < (size / 2) - 1; ++i, tmp = tmp->next);
            ListNode* first = tmp->next;
            tmp->next = NULL;
            head = this->sortList(head);
            first = this->sortList(first);
            head = this->mergeTwoLists(head, first);
            return head;
        }
    }
};
```
