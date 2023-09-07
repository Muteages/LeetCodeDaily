# Reverse Linked List II

https://leetcode.com/problems/reverse-linked-list-ii/description

Given the head of a singly linked list and two integers left and right where left <= right, reverse the nodes of the list from position left to position right, and return the reversed list.


## Approach 

``` C++
    ListNode* reverseBetween(ListNode* head, int left, int right) {
        if (left == right)
        {
            return head;
        }

        ListNode dummy(0, head);
        ListNode* prev = &dummy;
        
        for (int i = 0; i < left - 1; i++)
        {
            prev = prev->next;
        }

        ListNode* current = prev->next;
        // prev --> current --> next --> next.next
        for (int i = left; i < right; i++)
        { // Reverse the target list
            ListNode* next = current->next;
            current->next = next->next; // Disconnect the next node

            next->next = prev->next;  // Reverse current and next
            prev->next = next;        // Connect prev and next;
        }

        return dummy.next;
    }
```