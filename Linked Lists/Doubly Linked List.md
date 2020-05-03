💡 The doubly linked list is very similar to the singly linked list except for the difference of the previous pointer. In a doubly linked list, a node is made up of the following components.

* **Data**
* **Next** (Points to the next node)
* **Prev** (Points to the previous node)

\* The prev of the head node points to NULL while the next of the tail node also points to NULL.

```python
class Node:
    def __init__(self, data):
        self.data = data
        self.next = None
        self.prev = None

class DoublyLinkedList:
    def __init__(self):
        self.head = None
    
    def append(self, data):
        pass
    
    def prepend(self, data):
        pass
    
    def print_list(self):
        pass    
```

append
------

1\. The doubly linked list is empty.

2\. The doubly linked list is not empty.

```python
def append(self, data):
    if self.head is None:
        new_node = Node(data)
        new_node.prev = None
        self.head = new_node
    else:
        new_node = Node(data)
        curr = self.head
        while curr:
            curr = curr.next
        curr.next = new_node
        new_node.prev = curr
        new_node.next = None
```

print\_list
-----------

```python
def print_list(self):
    curr = self.head
    while curr:
        print(curr.data)
        curr = curr.next
```

prepend
-------

```python
def prepend(self, data):
    if self.head is None:
        new_node = Node(data)
        new_node.prev = None
        self.head = new_node
    else:
        new_node = Node(data)
        self.head.prev = new_node
        new_node.next = self.head
        self.head = new_node
        new_node.prev = None
```

Add Node After
---------------

1\. The node that we have to insert after the new node is the last node in the doubly linked list so that the next of that node is NULL. We will call the **append** method, to insert a node after this node.

2\. The node that we have to insert after the new node is not the last node in the doubly linked list.

```python
def add_after_node(self, key, data):
    curr = self.head
    while curr:
        if curr.next is None and curr.data == key:
            self.append(data)
            return
        elif curr.data == key:
            new_node = Node(data)
            nxt_tmp = curr.next
            curr.next = new_node
            new_node.next = nxt_tmp
            nxt_tmp.prev = new_node
            new_node.prev = curr
            return
        curr = curr.next
```

Add Node Before
---------------

```python
def add_before_node(self, key, data):
        curr = self.head
        while curr:
            if curr.next is None and curr.data == key:
                self.prepend(data)
                return
            elif curr.data == key:
                new_node = Node(data)
                prev_tmp = curr.prev
                prev_tmp.next = new_node
                curr.prev = new_node
                new_node.next = curr
                new_node.prev = prev_tmp
                return
            curr = curr.next
            # FIX: Does not work when 
            # Adding node before last node
```

Delete Node
-----------

1\. Deleting the only node present

2\. Deleting Head Node

3\. Deleting node other than head where **curr.next** is not **None**

4\. Deleting node other than head where **curr.next** is **None**

```python
# Case 1
def delete(self, key):
    curr = self.head
    while curr:
        if curr.data == key and curr == self.head and not curr.next:
            curr = None
            self.head = None
            return
        curr = curr.next
```



