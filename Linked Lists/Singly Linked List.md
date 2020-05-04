Implementation — Python 3.7.0
-----------------------------

```python
class Node:
    def __init__(self, data):
        self.data = data
        self.next = None
        
class LinkedList:
    def __init__(self):
        self.head = None
    
    def print_list(self):
        curr = self.head
        while curr:
            print(curr.data)
            curr = curr.next
    
    def prepend(self, data):
        new_node = Node(data)
        new_node.next = self.head
        self.head = new_node
        
    def append(self, data):
        new_node = Node(data)
        if self.head is None:
            self.head = new_node
            return
        curr = self.head
        while curr.next:
            curr = curr.next
        # Curr should now be last not None Node.
        curr.next = new_node
        
    def insert_after(self, node_val, data):
        """Precondition: Node with node_val data exists"""
        new_node = Node(data)
        curr = self.head
        while curr.data != node_val:
            curr = curr.next
        # Curr is now at previous node from insertion
        tmp_node = curr.next
        curr.next = new_node
        new_node.next = tmp_node
        
    def delete_node(self, node_val):
        """Precondition: Node with node_val data exists"""
        # Case 1. If node_val is self.head.data
        if (self.head.data == node_val):
            old_head = self.head
            self.head = self.head.next
            del old_head
            return
        # Case 2. If node_val is not self.head.data
        curr = self.head
        while curr.next.data != node_val:
            curr = curr.next
        node_to_del = curr.next
        curr.next = curr.next.next
        del node_to_del
    
    def delete_node_at_pos(self, pos):
        # 1. Node to be deleted is at position 0
        # 2. Node to be deleted is not at position 0
        if self.head:
            curr = self.head
            if pos == 0:
                self.head = curr.next
                curr = None
                return
        prev = None
        count = 0
        while curr and count != pos:
            prev = curr
            curr = curr.next
            count += 1
        
        if curr is None:
            return
        prev.next = curr.next
        curr = None
        
    def __len__(self):
        curr = self.head
        count = 0
        while curr is not None:
            count += 1
            curr = curr.next
        return count
    
    def len_recursive(self, node):
        if node is None:
            return 0
        return 1 + self.len_recursive(node.next)
```

Node Swap
---------

```python
def swap_node(self, node1, node2):
    
    # If nodes to swap are the same, do not swap. Simply return
    if node1 == node2:
        return
    
    # Loop until curr_1 does not point to node1
    prev_1 = None
    curr_1 = self.head
    while curr_1 and curr_1.data != node1:
        prev_1 = curr_1
        curr_1 = curr_1.next
    
    # Loop until curr_2 does not point to node2
    prev_2 = None
    curr_2 = self.head
    while curr_2 and curr_2.data != node2:
        prev_2 = curr_2
        curr_2 = curr_2.next
    
    
    # Case if any of pointers is None. Swap is not possible. Simply return
    if not curr_1 or not curr_2:
        return
    
    
    # Handling previous nodes links
    if prev_1:
        prev_1.next = curr_2
    else:
        self.head = curr_2
    
    if prev_2:
        prev_2.next = curr_1
    else:
        self.head = curr_1
    
    # Handling next nodes links
    # Python's one liner swap magic
    curr_1.next, curr_2.next = curr_2.next, curr_1.next
```

Reversing
---------

```python
def reverse_iterative(self):
    prev = None
    curr = self.head
    while curr is not None:
        next_tmp = curr.next
        curr.next = prev
        prev = curr
        curr = next_tmp
    self.head = prev
```

```python
def reverse_recursive(self):
    
    def _reverse_recursive(cur, prev):
        if not cur:
            return prev
        nxt = cur.next
        cur.next = prev
        prev = cur
        cur = nxt
        return _reverse_recursive(cur, prev)
    
    self.head = _reverse_recursive(cur=self.head, prev=None)
```

Merge Two Sorted Linked Lists
-----------------------------

```python
def merge_sorted(self, llist):
    p = self.head
    q = llist.head
    s = None
    
    if not p:
        return q
    if not q:
        return p
    
    # Make the new_head the smallest value checking p->node and q->node
    if p and q:
        if p.data <= q.data:
            s = p
            p = s.next
        else:
            s = q
            q = s.next
        new_head = s # new_head
    
    while p and q:
        if p.data <= q.data:
            s.next = p
            s = p
            p = s.next
        else:
            s.next = q
            s = q
            q = s.next
            
    if not p:
        s.next = q
    if not q:
        s.next = p
    return new_head
```

Removing Duplicates
-------------------

```python
def remove_duplicates(self):
    curr = self.head
    prev = None
    dup_values = {}
    
    while curr:
        if curr.data in dup_values:
            # remove node
            prev.next = curr.next
            curr = None
        else:
            # have not encountered element before
            dup_values[curr.data] = 1
            prev = curr
        curr = prev.next
        
```

Nth-to-Last Node
----------------

Get the Nth-to-Last Node from a given linked list given **n**.

```python
"""
2 pointers: p, q
p --> head node
q --> n nodes beyond head node
"""
def nth_last(self, n):
    curr = self.head
    p = self.head
    count = 0
    while count != n:
        if curr is None:
            print("This n would bring you to the head. Where everything begins.")
            return self.head.data
        count += 1
        curr = curr.next
    q = curr # q will not point at the node that is n positions beyond head
    while q is not None:
        q = q.next
        p = p.next
    return p.data
```

Count Occurence Recursively
---------------------------

```python
def count_occurence_recursive(self, node, data):
    if not node:
        return 0
    if node.data == data:
        return 1 + self.count_occurence_recursive(node.next, data)
    else:
        return self.count_occurence_recursive(node.next, data)
```

Rotate
------

Shifting or rotating everything that follows the pivot node to the front of the linked list.

1-\>2-\>3-\>4-\>5, rotated by pivot 3 ↵ 

4-\>5-\>1-\>2-\>3

```python
def rotate(self, k):
    if self.head and self.head.next:
        p = self.head
        q = self.head
        prev = None
        count = 0
    while p and count < k:
        prev = p
        p = p.next
        q = q.next
        count += 1
    p = prev
    while q:
        prev = q
        q = q.next
    q = prev
    
    q.next = self.head
    self.head = p.next
    p.next = None
```

Is Palindrome
-------------

```python
# Solution 1: Using a string
def is_palindrome(self):
    s = ""
    p = self.head
    while p:
        s += p.data
        p = p.next
    return s == s[::-1]
```

```python
# Solution 2: Using a stack
def is_palindrome(self):
    p = self.head
    s = []
    while p:
        s.append(p.data)
        p = p.next
    p = self.head
    while p:
        data = s.pop()
        if p.data != data:
            return False
        p = p.next
    return True
```

Move Tail to Head
-----------------

1-\>2-\>3-\>4

4-\>1-\>2-\>3

```python
def move_tail_to_head(self):
    if self.head and self.head.next:
        curr = self.head
        prev = None
        while curr.next:
            prev = curr
            curr = curr.next
        curr.next = self.head
        self.head = curr
        prev.next = None
```

Sum Two Linked Lists
--------------------

```python
def sum_two_lists(self, llist):
        num1 = ""
        curr = self.head
        while curr is not None:
            num1 += str(curr.data)
            curr = curr.next
        num2 = ""
        curr = llist.head
        while curr is not None:
            num2 += str(curr.data)
            curr = curr.next
        num1 = num1[::-1]
        num2 = num2[::-1]
        return int(num1) + int(num2)
    
def sum_two_lists_S(self, llist):
    p = self.head
    q = llist.head
    
    sum_llist = LinkedList()
    
    carry = 0
    while p or q:
        if not p:
            i = 0
        else:
            i = p.data
        if not q:
            j = 0
        else:
            j = q.data
        s = i + j + carry
        if s >= 10:
            carry = 1
            remainder = s % 10
            sum_llist.append(remainder)
        else:
            carry = 0
            sum_llist.append(s)
        if p:
            p = p.next
        if q:
            q = q.next
    return sum_llist
```

Complete Code
-------------

```python
class Node:
    def __init__(self, data):
        self.data = data
        self.next = None

class LinkedList:
    def __init__(self):
        self.head = None
    
    def print_list(self):
        curr = self.head
        while curr:
            print(curr.data)
            curr = curr.next
    
    def print_rec(self, node):
        if node is None:
            return
        print(node.data)
        self.print_rec(node.next)
        
    def prepend(self, data):
        new_node = Node(data)
        new_node.next = self.head
        self.head = new_node
        
    def append(self, data):
        new_node = Node(data)
        if self.head is None:
            self.head = new_node
            return
        curr = self.head
        while curr.next:
            curr = curr.next
        curr.next = new_node
        
    def insert_after(self, node_val, data):
        """Precondition: node_val exists"""
        new_node = Node(data)
        curr = self.head
        while curr.data != node_val:
            curr = curr.next
        tmp_node = curr.next
        curr.next = new_node
        new_node.next = tmp_node
        
    def delete_node(self, node_val):
        """Precondition: node_val exists"""
        # Case 1. If node_val is self.head.data
        if (self.head.data == node_val):
            old_head = self.head
            self.head = self.head.next
            del old_head
            return
        # Case 2. If node_val is not self.head.data
        curr = self.head
        while curr.next.data != node_val:
            curr = curr.next
        node_to_del = curr.next
        curr.next = curr.next.next
        del node_to_del
        
    def delete_node_at_pos(self, pos):
        if self.head:
            curr = self.head
        # Case 1. Node to be deleted is at position 0
            if pos == 0:
                self.head = curr.next
                curr = None
                return
        # Case 2. Node to be deleted is not at position 0
        prev = None
        count = 0
        while curr and count != pos:
            prev = curr
            curr = curr.next
            count += 1
        
        if curr is None:
            return
        prev.next = curr.next
        curr = None
        
    def __len__(self):
        curr = self.head
        count = 0
        while curr is not None:
            count += 1
            curr = curr.next
        return count
        
    def len_recursive(self, node):
        if node is None:
            return 0
        return 1 + self.len_recursive(node.next)
        
    def swap_node(self, node1, node2):
        if node1 == node2:
            return
        prev_1 = None
        curr_1 = self.head
        while curr_1 and curr_1.data != node1:
            prev_1 = curr_1
            curr_1 = curr_1.next
        prev_2 = None
        curr_2 = self.head
        while curr_2 and curr_2.data != node2:
            prev_2 = curr_2
            curr_2 = curr_2.next
        
        if not curr_1 or not curr_2:
            return
        
        if prev_1:
            prev_1.next = curr_2
        else:
            self.head = curr_2
        
        if prev_2:
            prev_2.next = curr_1
        else:
            self.head = curr_1
        
        curr_1.next, curr_2.next = curr_2.next, curr_1.next
        
    def reverse(self):
        prev = None
        curr = self.head
        while curr:
            next_tmp = curr.next
            curr.next = prev
            prev = curr
            curr = next_tmp
        self.head = prev
    
    def reverse_recursive(self):
        def _reverse_recursive(cur, prev):
            if not cur:
                return prev
            
            nxt = cur.next
            cur.next = prev
            prev = cur
            cur = nxt
            return _reverse_recursive(cur, prev)
        self.head = _reverse_recursive(cur=self.head, prev=None)
        
    def reverse_recursive_2(self, head):
        if head is None:
            return None
        elif head.next is None:
            return head
        else:
            nextNode = head.next
            head.next = None
            rest = self.reverse_recursive_2(nextNode)
            nextNode.next = head
            return rest
    
    def merge_sorted(self, llist):
        """Precondition: self and llist are sorted."""
        p = self.head
        q = llist.head
        s = None
        if not p:
            return q
        if not q:
            return p
            
        if p and q:
            if p.data <= q.data:
                s = p
                p = s.next
            else:
                s = q
                q = s.next
            new_head = s
        
        while p and q:
            if p.data <= q.data:
                s.next = p
                s = p
                p = s.next
            else:
                s.next = q
                s = q
                q = s.next
        if not p:
            s.next = q
        if not q:
            s.next = p
        
        return new_head
        
    def remove_duplicates(self):
        curr = self.head
        prev = None
        dup_values = {}
        
        while curr:
            if curr.data in dup_values:
                # Remove Node:
                prev.next = curr.next
                curr = None
            else:
                # Have not encountered element before
                dup_values[curr.data] = 1
                prev = curr
            curr = prev.next
    
    def nth_last(self, n):
        # P, Q pointers
        # P --> head, Q --> n nodes beyond head node
        curr = self.head
        p = self.head
        count = 0
        while count != n:
            if curr is None:
                print("This n would bring you back to the head node.")
                return self.head.data
            count += 1
            curr = curr.next
        q = curr
        while q is not None:
            q = q.next
            p = p.next
        return p.data
        
    def nth_last_len(self, n):
        total_len = self.len_recursive(self.head)
        curr = self.head
        while curr:
            if total_len == n:
                return curr.data
            total_len -= 1
            curr = curr.next
        if curr is None:
            return
        
    def count_occurence(self, node_val):
        count = 0
        curr = self.head
        while curr:
            if curr.data == node_val:
                count += 1
            curr = curr.next
        return count
        
    def count_occurence_recursive(self, node, data):
        if not node:
            return 0
        if node.data == data:
            return 1 + self.count_occurence_recursive(node.next, data)
        else:
            return self.count_occurence_recursive(node.next, data)
    
    def rotate(self, k):
        if self.head and self.head.next:
            p = self.head
            q = self.head
            prev = None
            count = 0
        while p and count < k:
            prev = p
            p = p.next
            q = q.next
            count += 1
        p = prev
        while q:
            prev = q
            q = q.next
        q = prev
        
        q.next = self.head
        self.head = p.next
        p.next = None
```

