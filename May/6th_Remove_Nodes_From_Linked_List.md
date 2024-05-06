# Remove Nodes from Linked List

https://leetcode.com/problems/remove-nodes-from-linked-list

You are given the head of a linked list.

Remove every node which has a node with a greater value anywhere to the right side of it.

Return the head of the modified linked list.

## Approach 1

``` C++
    ListNode* removeNodes(ListNode* head) {
        ListNode* dummyHead = new ListNode(1e5 + 1, head);
        std::stack<ListNode*> st;
        st.emplace(dummyHead);
        ListNode* curr = head;
        while (curr && curr->next)
        {
            if (curr->val >= curr->next->val)
            { // Keep the current node
                st.emplace(curr);
            }
            else
            { // Remove the current node
                while (st.top()->val < curr->next->val)
                { // Backtrace the list, remove all nodes smaller than next node
                    st.pop();
                }
                st.top()->next = curr->next;
            }
            curr = curr->next;
        }
        return dummyHead->next;
    }
```

## Approach 2

``` C++
    ListNode* removeNodes(ListNode* head) {
        if (!head)
        {
            return nullptr;
        }
        head->next = removeNodes(head->next);
        if (head->next && head->next->val > head->val)
        { // Skip the cuurent node
            return head->next;
        }
        else
        { // Keep the current node
            return head;
        }
    }
```