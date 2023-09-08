# 86 Partition List

https://leetcode.com/problems/partition-list/description/

Given the head of a linked list and a value x, partition it such that all nodes less than x come before nodes greater than or equal to x.

You should preserve the original relative order of the nodes in each of the two partitions.

## Approach 1 
Modify the list in place. Traverse the list and move all small node to the left side of the first node which greater than or equal to x

``` C++
    ListNode* partition(ListNode* head, int x) {
        if (!head)
        {
            return nullptr;
        }

        ListNode* curNode = head;
        ListNode* curPrev = nullptr;  

        ListNode* insertPrev = nullptr;
        ListNode* insertNext = nullptr;  // the first node which is greater than x

        // Two cases: 1.  First number is x and rest of numbers are greater than it.
        //            2.  Normal case
        while (curNode)
        { // Insert elements at the position where the previous val is less than x and the next node is greater than x
            if (curNode->val >= x)
            {
                if (insertNext == nullptr)
                {
                    insertNext = curNode;
                    insertPrev = curPrev;
                }
            }
            else if (insertNext)
            { // update the list
                prev->next = curNode->next;
                if (insertPrev == nullptr)
                { // insert the node at the head
                    head = curNode;
                    curNode->next = insertNext;
                    insertPrev = curNode;
                }
                else
                { // normal case
                    insertPrev->next = curNode;
                    curNode->next = insertNext;
                    insertPrev = curNode;
                }
            }

            curPrev = curNode;
            curNode = curNode->next;
        }

        return head;
    } 
```

## Approach 2 
Creat two new list: small and great, return the merged list

``` C++
ListNode* partition(ListNode* head, int x) {
        if (!head)
        {
            return nullptr;
        }

        ListNode* small = new ListNode(-1);
        ListNode* great = new ListNode(-1);
        ListNode* curSmall = small;
        ListNode* curGreat = great;

        while (head)
        {
            if (head->val < x)
            { // add to small list
                curSmall->next = head;
                curSmall = head;
            }
            else
            {
                curGreat->next = head;
                curGreat = head;
            }

            head = head->next;
        }

        // Merge two lists
        curSmall->next = great->next;
        curGreat->next = nullptr;

        return small->next;
    }



```