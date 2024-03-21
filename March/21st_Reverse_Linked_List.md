# Reverse Linked List

https://leetcode.com/problems/reverse-linked-list

Given the head of a singly linked list, reverse the list, and return the reversed list.

## Approach 1

Iteration

```C++
    ListNode* reverseList(ListNode* head) {
        if (!head || !head->next)
        {
            return head;
        }

        ListNode* prev = nullptr;
        ListNode* curr = head;
        while (curr)
        {
            ListNode* next = curr->next;
            curr->next = prev;
            prev = curr;
            curr = next;
        }
        return prev;
    }
```

## Approach 2

Recursion
``` C++
    ListNode* reverseList(ListNode* prev, ListNode* curr)
    {
        if (!curr)
        {
            return prev;
        }
        ListNode* next = curr->next;
        curr->next = prev;
        return reverseList(curr, next);
    }
    ListNode* reverseList(ListNode* head) {
        if (!head || !head->next)
        {
            return head;
        }
        return reverseList(nullptr, head);
    }
```
