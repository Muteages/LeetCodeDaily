# Split Linked List in Parts

https://leetcode.com/problems/split-linked-list-in-parts

Given the head of a singly linked list and an integer k, split the linked list into k consecutive linked list parts.

The length of each part should be as equal as possible: no two parts should have a size differing by more than one. This may lead to some parts being null.

The parts should be in the order of occurrence in the input list, and parts occurring earlier should always have a size greater than or equal to parts occurring later.

Return an array of the k parts.


## Approach 1

``` C++
    int getLength(ListNode* node)
    {
        int len = 0;
        while (node)
        {
            len++;
            node = node->next;
        }
        return len;
    }

    vector<ListNode*> splitListToParts(ListNode* head, int k) {
        int len = getLength(head);
        std::vector<ListNode*> ans(k, nullptr);
        auto [q, r] = std::div(len, k);
        ListNode* next{};
        for (int i = 0; i < k && head; i++)
        {
            ans[i] = head;
            int sz = q + (r-- > 0);

            for (int j = 0; j < sz - 1; j++)
            {
                head = head->next;
            }
            next = head->next;
            head->next = nullptr;
            head = next;
        }
        return ans;
    }
```

``` JavaScript
const getLength = (head) => {
    let len = 0;
    while (head) {
        len++;
        head = head.next;
    }
    return len;
};

var splitListToParts = function(head, k) {
    const len = getLength(head);
    let ans = Array(k).fill(null);
    let sz = Math.floor(len / k), extra = len % k;
    let next = head;
    for (let i = 0; i < k && head; i++) {
        ans[i] = head;
        let curSize = sz + (extra-- > 0);
        for (let j = 0; j < curSize - 1; j++) {
            head = head.next;
        }
        next = head.next;
        head.next = null;
        head = next;
    }
    return ans;
};
```





