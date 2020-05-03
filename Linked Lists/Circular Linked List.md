💡 Similar to a **singly linked list**, except for the fact that the next of the tail node is the head node instead of null.

```python
class Node:
    def __init__(self, data):
        self.data = data
        self.next = None
        
class CircularLinkedList:
    def __init__(self):
        self.head = None
        
    def prepend(self, data):
        pass
    
    def append(self, data):
        pass

    def print_list(self):
        pass
```

append
------

Appending to a circular linked list implies inserting the new node after the node that was previously pointing to the head of the linked list.

```python
def append(self, data):
    if not self.head:
        self.head = Node(data)
        self.head.next= self.head
    else:
        new_node = Node(data)
        curr = self.head
        while curr.next != self.head:
            curr = curr.next
        curr.next = new_node
        new_node.next = self.head
```

print\_list
-----------

```python
def print_list(self):
    curr = self.head
    while curr:
        print(curr.data)
        curr = curr.next
        break if curr = self.head else pass
```

Prepend
-------

To prepend an element to the pinkest list implies to make it the head of the linked list.

1-\>2-\>3-\>4-\>5-\>**6**

 ^ —————---- ^

self.head = Node(1)

```python
def prepend(self, data):
    new_node = Node(data)
    curr = self.head
    new_node.next = self.head
    
    if not self.head:
        new_node.next = new_node
    else:
        while curr.next != self.head:
            curr = curr.next
        curr.next = new_node
    self.head = new_node
```

Remove Node
-----------

\# == Case where you want to remove the head node

1-\>1

2-\>1-\>3

Get to the last node.

\# if it is the same node. Make head None

\# it there are more nodes. Make the next of the last, the next of the head, make self.head.next the head

\# == Case where you want to remove a node other than head

Keep track of current node and previous node. Loop until the curr.next != head. Advance prev and cur.

IF the data in the current curr matches the data of the key to be deleted, make. The next of the previous, the next of the current. And make curr point to the next node of curr.

```python
def remove(self, key):
    if self.head:
        if self.head.data == key:
            curr= self.head
            while curr.next != self.head:
                curr = curr.next
            if self.head == self.head.next:
                self.head = None
            else:
                curr.next = self.head.next
                self.head = self.head.next
        else:
            curr = self.head
            prev = None
            while curr.next != self.head:
                prev = curr
                curr = curr.next
                if curr.data == key:
                    prev.next = curr.next
                    break
```

\_\_len\_\_()
-------------

```python
def __len__(self):
    curr = self.head
    count = 0
    while curr:
        count += 1
        curr = curr.next
        if curr == self.head:
            break
    return count
```

Split Linked List into Two Halves
---------------------------------

```python
def split_list(self):
    size = len(self)
    
    if size == 0:
        return None
    if size == 1:
        return self.head
        
    mid = size // 2
    count = 0
    
    prev = None
    curr = self.head
    
    while curr and count < mid:
        count += 1
        prev = curr
        curr = curr.next
    prev.next = self.head
    
    split_cllist = CircularLinked()
    while curr.next != self.head:
        split_cllist.append(curr.data)
        curr = curr.next
    split_cllist.append(curr.data)
    
    self.print_list()
    print("\n")
```

Is Circular Linked List
-----------------------

```python
def is_circular(self):
    # If any of the nodes is none.
    # Assume input_list is circular. Then it should not have any None nodes
    curr = self.head
    while curr:
        curr = curr.next
        if curr == self.head:
            return True
    return False
```

**NOTE: **Give that you have access to the head node, the time complexity of removing the head node in a circular linked list containing *n* elements is O(1) —\> **FALSE**. It is **O(n)**. (Need to reconnect the tail)

Complete Code
-------------

```python
class Node:
    def __init__(self, data):
        self.data = data
        self.next = None
        
class CircularLinkedList:
    def __init__(self):
        self.head = None
        
    def __len__(self):
        curr = self.head
        count = 0
        while curr:
            count += 1
            curr = curr.next
            if curr == self.head:
                break
        return count
        
    def prepend(self, data):
        new_node = Node(data)
        curr = self.head
        new_node.next = self.head
        
        if not self.head:
            new_node.next = new_node
        else:
            while curr.next != self.head:
                curr = curr.next
            curr.next = new_node
        self.head = new_node
    
    def append(self, data):
        if not self.head:
            self.head = Node(data)
            self.head.next = self.head
        else:
            new_node = Node(data)
            curr = self.head
            while curr.next != self.head:
                curr = curr.next
            curr.next = new_node
            new_node.next = self.head

    def print_list(self):
        curr = self.head
        while curr:
            print(curr.data)
            curr = curr.next
            if curr == self.head:
                break
                
    def print_list_rec(self, node):
        pass
        
                
    def remove(self, key):
        if self.head:
            if self.head.data == key:
                curr = self.head
                while curr.next != self.head:
                    curr = curr.next
                if self.head == self.head.next:
                    self.head = None
                else:
                    curr.next = self.head.next
                    self.head = self.head.next
            else:
                curr = self.head
                prev = None
                while curr.next != self.head:
                    prev = curr
                    curr = curr.next
                    if curr.data == key:
                        prev.next = curr.next
                        break
                    
    def split_list(self):
        size = len(self)
        if size == 0:
            return None
        if size == 1:
            return self.head
        
        mid = size // 2
        count = 0
        
        prev = None
        curr = self.head
        while curr and count < mid:
            count += 1
            prev = curr
            curr = curr.next
        prev.next = self.head
        
        split_cllist = CircularLinkedList()
        while curr.next != self.head:
            split_cllist.append(curr.data)
            curr = curr.next
        split_cllist.append(curr.data)
        
        self.print_list()
        print("\n")
        split_cllist.print_list()
    
    def remove_node(self, node):
        if self.head == node:
            curr = self.head
            while curr.next != self.head:
                curr = curr.next
            if self.head == self.head.next:
                self.head = None
            else:
                curr.next = self.head.next
                self.head = self.head.next
        else:
            curr = self.head
            prev = None
            while curr.next != self.head:
                prev = curr
                curr = curr.next
                if curr == node:
                    prev.next = curr.next
                    curr = curr.next
                    
    def is_circular(self, other):
        curr = other.head
        while curr:
            curr = curr.next
            if curr == other.head:
                return True
        return False
                    
                    
    # Fun with josephus_circle                
    def josephus_circle(self, step):
        curr = self.head
        
        while len(self) > 1:
            count = 1
            while count != step:
                curr = curr.next
                count += 1
            print("KILL: " + str(curr.data))
            self.remove_node(curr)
            curr = curr.next
        print("The winner is: " + str(curr.data))
```





