# Insertion Sort List

https://leetcode.com/problems/insertion-sort-list/description/

Given the head of a singly linked list, sort the list using insertion sort, and return the sorted list's head.

## Approach 

``` C++
    ListNode* insertionSortList(ListNode* head) {
        if (!head || !head->next)
        {
            return head;
        }

        ListNode* sorted = nullptr;
        ListNode* curr = head;
        while (curr)
        {
            auto next = curr->next;
            sorted = insertNode(sorted, curr);
            curr = next;
            
        }
        return sorted;
    }

    ListNode* insertNode(ListNode* head, ListNode* node)
    {
        if (!head || node->val < head->val)
        { // Insert the node before head
            node->next = head;
            return node;
        }
        
        ListNode* curr = head;
        while (curr->next && curr->next->val < node->val)
        { // find the position to insert the node
            curr = curr->next;
        }
        // Update
        node->next = curr->next;
        curr->next = node;
        return head;
    }
```