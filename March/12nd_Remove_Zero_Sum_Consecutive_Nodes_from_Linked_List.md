# Remove Zero Sum Consecutive Nodes from Linked List

https://leetcode.com/problems/remove-zero-sum-consecutive-nodes-from-linked-list


Given the head of a linked list, we repeatedly delete consecutive sequences of nodes that sum to 0 until there are no such sequences.

After doing so, return the head of the final linked list.  You may return any such answer.

## Approach 1
``` C++
    ListNode* removeZeroSumSublists(ListNode* head) {
        ListNode dummy(0, head);
        std::unordered_map<int, ListNode*> prefix;
        prefix[0] = &dummy;
        int curSum = 0;
        ListNode* node = head;
        while (node)
        {
            curSum += node->val;
            if (prefix.count(curSum))
            { // Find a sequence which needs to be removed
                ListNode* remove = prefix[curSum]->next;
                int tempSum = curSum + remove->val;
                while (tempSum != curSum)
                { // Clean all record sum of this sequence
                    prefix.erase(tempSum);
                    remove = remove->next;
                    tempSum += remove->val;
                }
                // Update the linked list
                prefix[curSum]->next = remove->next;
            }
            else
            {
                prefix[curSum] = node;
            }
            node = node->next;
        }
        return dummy.next;
    }
```

## Approach 2

``` C++
    ListNode* removeZeroSumSublists(ListNode* head) {
        ListNode dummy(0, head);
        std::unordered_map<int, ListNode*> prefix;
        int sum = 0;
        ListNode* node = &dummy;
        while (node)
        {
            sum += node->val;
            prefix[sum] = node;
            node = node->next;
        }

        node = &dummy;
        sum = 0;
        while (node)
        {
            sum += node->val;
            node->next = prefix[sum]->next;
            node = node->next;
        }
        return dummy.next;
    }
```