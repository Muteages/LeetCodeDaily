# Insert Greatest Common Divisors in Linked List

https://leetcode.com/problems/insert-greatest-common-divisors-in-linked-list

Given the head of a linked list head, in which each node contains an integer value.

Between every pair of adjacent nodes, insert a new node with a value equal to the greatest common divisor of them.

Return the linked list after insertion.

## Approach 

``` C++
    ListNode* insertGreatestCommonDivisors(ListNode* head) {
        ListNode* prev = head, *curr = head->next;
        while (curr)
        {
            int divisor = std::gcd(prev->val, curr->val);
            ListNode* node = new ListNode(divisor, curr);

            // Rearrange the list
            prev->next = node;
            prev = curr;
            curr = curr->next;
        }
        return head;
    }
```

``` JavaScript
// Euclidean Algorithm
const getGCD = (a, b) => {
    while (b) {
        let div = a % b;
        a = b;
        b = div;
    }
    return a;
};
var insertGreatestCommonDivisors = function(head) {
    let prev = head, curr = head.next;
    while (curr) {
        let gcd = getGCD(prev.val, curr.val);
        let node = new ListNode(gcd, curr);

        prev.next = node;
        prev = curr;
        curr = curr.next; 
    }
    return head;
};
```