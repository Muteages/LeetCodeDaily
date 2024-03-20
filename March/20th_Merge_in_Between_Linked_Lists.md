# Merge in Between Linked Lists

https://leetcode.com/problems/merge-in-between-linked-lists

You are given two linked lists: list1 and list2 of sizes n and m respectively.

Remove list1's nodes from the ath node to the bth node, and put list2 in their place.

## Approach

``` C++
    ListNode* mergeInBetween(ListNode* list1, int a, int b, ListNode* list2) {
        ListNode* list2Tail = list2;
        // Find list2's end node
        while (list2Tail->next)
        {
            list2Tail = list2Tail->next;
        }

        int lenAB = b - a + 1;
        ListNode* current = list1;
        // Find the node before the removed section in list1
        while (a > 1)
        { 
            current = current->next;
            a--;
        }
        
        ListNode* temp = current->next;
        current->next = list2;
        current = temp;
        // Find the node after the removed section in list1
        while (lenAB)
        {
            current = current->next;
            lenAB--;
        }
        list2Tail->next = current;
        return list1;
    }
```