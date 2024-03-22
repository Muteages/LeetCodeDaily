# Palindrome Linked List

Given the head of a singly linked list, return true if it is a 
palindrome or false otherwise.

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
        return slow->next;
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
    bool isPalindrome(ListNode* head) {
        if (!head || !head->next)
        {
            return true;
        }

        ListNode* mid = getMidNode(head);
        mid = reverseList(mid);
        while (mid)
        {
            if (head->val != mid->val)
            {
                return false;
            }
            head = head->next;
            mid = mid->next;
        }
        return true;
    }
```