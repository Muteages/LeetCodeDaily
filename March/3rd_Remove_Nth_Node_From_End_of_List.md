# Remove Nth Node from End of List

https://leetcode.com/problems/remove-nth-node-from-end-of-list

Given the head of a linked list, remove the nth node from the end of the list and return its head.

## Approach 1

``` C++
    ListNode* removeNthFromEnd(ListNode* head, int n) {
        if (!head->next)
        {
            return nullptr;
        }
        int sz = 0;
        ListNode* curr = head;
        while (curr)
        {
            sz++;
            curr = curr->next;
        }

        int cnt = sz - n;
        if (cnt == 0)
        { // Remove the first node
            return head->next;
        }
        curr = head;
        while (--cnt > 0)
        {
            curr = curr->next;
        }
        curr->next = curr->next->next; // Remove the target node
        return head;
    }
```

## Approach 2

Follow up: solve it in one pass

``` C++
    ListNode* removeNthFromEnd(ListNode* head, int n) {
        if (!head->next)
        {
            return nullptr;
        }
        ListNode* slow = head;
        ListNode* fast = head;
        while (fast && n-- > 0)
        { // Initialise the fast node
            fast = fast->next;
        }
        if (!fast)
        { // Indicates the first node need to be removed since fast node is out of range
            return head->next;
        }

        while (fast->next)
        {
            slow = slow->next;
            fast = fast->next;
        }

        slow->next = slow->next->next;
        return head;
    }
```