# Double a Number Represented as a Linked List

https://leetcode.com/problems/double-a-number-represented-as-a-linked-list

You are given the head of a non-empty linked list representing a non-negative integer without leading zeroes.

Return the head of the linked list after doubling it.

 


## Approach 1

2 pass, using stack 
``` C++
    ListNode* doubleIt(ListNode* head) {
        std::stack<ListNode*> st;
        ListNode* curr = head;
        while (curr)
        {
            st.emplace(curr);
            curr = curr->next;
        }

        int carry = 0;
        while (!st.empty())
        {
            curr = st.top();
            st.pop();
            if (curr->val >= 5)
            {
                curr->val = (curr->val * 2 + carry) % 10;
                carry = 1;
            }
            else 
            {
                curr->val = curr->val * 2 + carry;
                carry = 0;
            }
        }
        if (carry == 1)
        {
            ListNode* newHead = new ListNode(1, head);
            return newHead;
        }
        else
        {
            return head;
        }
    }
```

## Approach 2

1 pass. two pointers
``` C++
    ListNode* doubleIt(ListNode* head) {
        if (head->val >= 5)
        { // Need to create a new head node
            head = new ListNode(0, head);
        }
        ListNode* prev = head;
        ListNode* curr = head;
        while (curr)
        {
            if (curr->val >= 5)
            { // Has carry, update the previous node
                prev->val++;
            }
            curr->val = (curr->val * 2) % 10;
            prev = curr;
            curr = curr->next;
        }
        return head;
    }
```

## Approach 3

Recursion

``` C++
    ListNode* doubleIt(ListNode* head) {
        if (hasCarry(head))
        {
            head = new ListNode(1, head);
        }
        return head;
    }

    int hasCarry(ListNode* node)
    {
        if (!node)
        {
            return false;
        }

        int num = node->val * 2 + hasCarry(node->next);
        node->val = num % 10;
        return num / 10;
    }
```

