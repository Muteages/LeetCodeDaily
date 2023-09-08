# Split Linked List in Parts

https://leetcode.com/problems/split-linked-list-in-parts/description

Given the head of a singly linked list and an integer k, split the linked list into k consecutive linked list parts.

The length of each part should be as equal as possible: no two parts should have a size differing by more than one. This may lead to some parts being null.

The parts should be in the order of occurrence in the input list, and parts occurring earlier should always have a size greater than or equal to parts occurring later.

Return an array of the k parts.


## Approach 1

``` C++
   vector<ListNode*> splitListToParts(ListNode* head, int k) {
        if (!head)
        {
            return std::vector<ListNode*>(k);
        }

        std::vector<ListNode*> list;
        while (head)
        {
            list.push_back(head);
            head = head->next;
        }

        int n = list.size();
        std::vector<ListNode*> ans(k);
        if (k >= n)
        { // Insert nodes one by one 
            for (int i = 0; i < n; i++)
            {
                ans[i] = list[i];
                ans[i]->next = nullptr;
            }
        }
        else
        {   // Calculate partitions
            int num = n / k;
            int rem = n % k;
            int curTail = -1;
            int curHead = 0;
            for (int i = 0; i < k; i++)
            {
                // Modify the current partition
                curTail += num;
                if (rem)
                { // if remainder exists, add an extra number in the current partition
                    curTail++;
                    rem--;
                }

                list[curTail]->next = nullptr;
                ans[i] = list[curHead];
                curHead = curTail + 1;
            }
        }
        return ans;
    }
```

## Approach 2

Instead create an extra vector, simply reloop the linked list

``` C++
   vector<ListNode*> splitListToParts(ListNode* head, int k) {
        int n = 0;
        ListNode* node = head;
        while (node)
        {
            n++;
            node = node->next;
        }

        std::vector<ListNode*> ans(k, nullptr);
        int partSize = n / k;
        int rem = n % k;
        node = head;
        ListNode* prev = nullptr;
        for (int i = 0; node && i < k; i++)
        {
            int curSize = partSize + (rem > 0);
            rem--;
            ans[i] = node;

            for (int j = 0; j < curSize; j++)
            {
                prev = node;
                node = node->next;
            }

            prev->next = nullptr;
        }

        return ans;
    }
```


