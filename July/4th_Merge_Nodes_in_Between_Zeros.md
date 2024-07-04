# Merge Nodes in Between Zeros

https://leetcode.com/problems/merge-nodes-in-between-zeros

You are given the head of a linked list, which contains a series of integers separated by 0's. The beginning and end of the linked list will have Node.val == 0.

For every two consecutive 0's, merge all the nodes lying in between them into a single node whose value is the sum of all the merged nodes. The modified list should not contain any 0's.

Return the head of the modified linked list.

## Approach 

``` C++
    ListNode* mergeNodes(ListNode* head) {
        int sum = 0;
        ListNode* prev = head->next, *curr = head->next;
        while (curr)
        {
            if (curr->val == 0)
            { // Merge point
                prev->val = sum;
                prev->next = curr->next;
                prev = curr->next;
                sum = 0;
            }
            else
            {
                sum += curr->val;
            }
            curr = curr->next;
        }
        return head->next;
    }
```

``` JavaScript
var mergeNodes = function(head) {
    let prev = head.next, curr = head.next, sum = 0;
    while (curr) {
        if (curr.val === 0) {
            prev.val = sum;
            prev.next = curr.next;
            prev = curr.next;
            sum = 0;
        }
        else {
            sum += curr.val;
        }
        curr = curr.next;
    }
    return head.next;
};
```