# Delete Nodes from Linked List Present in Array

https://leetcode.com/problems/delete-nodes-from-linked-list-present-in-array

You are given an array of integers nums and the head of a linked list. Return the head of the modified linked list after removing all nodes from the linked list that have a value that exists in nums.

## Approach 

Maintain a prev ptr
``` C++
    ListNode* modifiedList(vector<int>& nums, ListNode* head) {
        std::unordered_set<int> us(nums.begin(), nums.end());
        ListNode dummy(0, head);
        ListNode* prev = &dummy;
        while (head)
        {
            if (us.count(head->val))
            {
                prev->next = head->next;
            }
            else
            {
                prev = head;
            }
            head = head->next;
        }
        return dummy.next;
    }
```

Maintain a curr ptr

``` C++
    ListNode* modifiedList(vector<int>& nums, ListNode* head) {
        std::unordered_set<int> us(nums.begin(), nums.end());
        ListNode dummy(0);
        ListNode* curr = &dummy;
        while (head)
        {
            if (!us.count(head->val))
            {
                curr->next = head;
                curr = curr->next;
            }
            head = head->next;
        }
        curr->next = nullptr; // Break the last node
        return dummy.next;
    }
```

``` JavaScript
var modifiedList = function(nums, head) {
    const s = new Set(nums);
    let dummy = new ListNode(0, head);
    let prev = dummy;
    while (head)
    {
        if (s.has(head.val)) {
            prev.next = head.next;
        }
        else {
            prev = head;
        }
        head = head.next;
    }
    return dummy.next;
};
```
