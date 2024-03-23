# Reorder List

https://leetcode.com/problems/reorder-list

You are given the head of a singly linked-list. The list can be represented as:

L0 → L1 → … → Ln - 1 → Ln
Reorder the list to be on the following form:

L0 → Ln → L1 → Ln - 1 → L2 → Ln - 2 → …
You may not modify the values in the list's nodes. Only nodes themselves may be changed.


## Approach

``` C++
    ListNode* getMidNode(ListNode* head)
    {
        ListNode* slow = head, *fast = head;
        while (fast->next && fast->next->next)
        {
            slow = slow->next;
            fast = fast->next->next;
        }
        return slow;
    }

    ListNode* reverseList(ListNode* head)
    {
        ListNode* prev = nullptr, *next = nullptr;
        while (head)
        {
            next = head->next;
            head->next = prev;
            prev = head;
            head = next;
        }
        return prev;
    }
    void reorderList(ListNode* head) {
        if (!head->next || !head->next->next)
        {
            return;
        }

        ListNode* mid = getMidNode(head);
        ListNode* secondHalfHead = reverseList(mid->next);
        mid->next = nullptr; // Disconnect the first half list

        ListNode* curr1 = head, *curr2 = secondHalfHead;
        while (curr1 && curr2)
        {
            ListNode* next1 = curr1->next, *next2 = curr2->next;
            curr1->next = curr2;
            curr2->next = next1;
            curr1 = next1;
            curr2 = next2;
        }
    }
```