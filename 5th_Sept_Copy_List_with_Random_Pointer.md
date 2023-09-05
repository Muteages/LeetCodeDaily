# Copy List with Random Pointer

https://leetcode.com/problems/copy-list-with-random-pointer/description

A linked list of length n is given such that each node contains an additional random pointer, which could point to any node in the list, or null.

Construct a deep copy of the list. The deep copy should consist of exactly n brand new nodes, where each new node has its value set to the value of its corresponding original node. Both the next and random pointer of the new nodes should point to new nodes in the copied list such that the pointers in the original list and copied list represent the same list state. None of the pointers in the new list should point to nodes in the original list.

For example, if there are two nodes X and Y in the original list, where X.random --> Y, then for the corresponding two nodes x and y in the copied list, x.random --> y.

Return the head of the copied linked list.

The linked list is represented in the input/output as a list of n nodes. Each node is represented as a pair of [val, random_index] where:

val: an integer representing Node.val
random_index: the index of the node (range from 0 to n-1) that the random pointer points to, or null if it does not point to any node.
Your code will only be given the head of the original linked list.



## Approach 1

Maintain a map which define the old nodes and copied nodes

``` C++
    Node* copyRandomList(Node* head) {
        if (!head)
        {
            return nullptr;
        }
        std::unordered_map<Node*, Node*> mp; // old node - copy node

        Node* curNode = head;
        while (curNode)
        { // Initialise the map
            mp[curNode] = new Node(curNode->val);
            curNode = curNode->next;
        }

        // Reloop the original linked list
        curNode = head;
        while (curNode)
        {
            mp[curNode]->next = mp[curNode->next];
            mp[curNode]->random = mp[curNode->random];
            curNode = curNode->next;
        }
        return mp[head];
    }
```


## Approach 2

Interwave list: copy the node first and connect it with the original one like A->A*->B->B*. Then split them.

``` C++
    Node* copyRandomList(Node* head) {
        if (!head)
        {
            return nullptr;
        }

        Node* curNode = head;

        // Maintain the next relationship
        while (curNode)
        {   // Link the copied node next to the original node
            Node* temp = new Node(curNode->val);
            temp->next = curNode->next;
            curNode->next = temp;
            curNode = temp->next;
        }

        // Maintain the random relationship
        curNode = head;
        while (curNode)
        {
            if (curNode->random)
            {
                curNode->next->random = curNode->random->next;
            }
            curNode = curNode->next->next;
        }

        // Split original list and copy list
        Node* newHead = head->next;
        Node* curNewNode = newHead;
        Node* curOldNode = head;

        
        // Split original list and copy list
        while (curOldNode)
        {
            curOldNode->next = curOldNode->next->next;
            curNewNode->next = curNewNode->next ? curNewNode->next->next : nullptr;
            curOldNode = curOldNode->next;
            curNewNode = curNewNode->next;
        }

        return newHead;
    }
```

