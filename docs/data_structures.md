# Data Structures

## Linked Lists

### Single-linked list

#### Definition

``` python
class ListNode:
    def __init__(self, x):
        self.val = x
        self.next = None
```

#### Cycle Detection

=== "Intuition"

    The Floyd Algorithm aka Slow Fast Algorithm solves this problem.

    1. We use two pointers in the linked list.
    2. We traverse the linked list with both of the pointers.
    3. The first pointer advances two steps each time, and the other one step. They advance alternating.
    4. If at any point the "slower" pointer is in the next two fields of the "faster" pointer, the linked list has a cycle.
    5. Otherwise if the "faster" reaches the end of the linked list (next is empty), then there is no cycle.

=== "Algorithm"

    ``` python
    def hasCycle(self, head: Optional[ListNode]) -> bool:
        if head is None:
            return False
        slow = head
        fast = head
        while True:
            # advance fast 2 steps
            if fast.next is not None:
                if fast.next == slow:
                    return True
                if fast.next.next is not None:
                    if fast.next.next == slow:
                        return True
                    fast = fast.next.next
                else:
                    return False
            else:
                return False
            # advance slow 1 step
            if slow.next is not None:
                slow = slow.next
            else:
                # unlikely case
                return False
    ```

## Trees

### Binary Tree

#### Definition

``` python 
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right
```

#### Find max depth
=== "Intuition"

    * Use recursion to recursively go down each branch of the tree.
    * In each iteration increase by one.
    * Compare both sides at the top and take the larger sum of paths.

=== "Algorithm"

    ``` python
    def maxDepth(root: Optional[TreeNode]) -> int:
        return 0 if root is None else max(self.maxDepth(root.left), self.maxDepth(root.right)) + 1
    ```