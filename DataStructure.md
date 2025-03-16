# 数据结构教程

这个教程介绍了几种常见的数据结构，并通过代码示例进行讲解。这些数据结构包括：

- 链表（Linked List）
- 栈（Stack）
- 队列（Queue）

每个数据结构都有详细的注释和示例代码，帮助你理解每个数据结构的工作原理。

### 链表

链表是一种线性数据结构，其中每个元素是一个节点，节点包含数据和指向下一个节点的引用。

```python name=linked_list.py
class Node:
    def __init__(self, data):
        self.data = data
        self.next = None

class LinkedList:
    def __init__(self):
        self.head = None

    def append(self, data):
        new_node = Node(data)
        if not self.head:
            self.head = new_node
            return
        last = self.head
        while last.next:
            last = last.next
        last.next = new_node

    def print_list(self):
        current = self.head
        while current:
            print(current.data, end=" -> ")
            current = current.next
        print("None")

# 示例
llist = LinkedList()
llist.append(1)
llist.append(2)
llist.append(3)
llist.print_list()
```

### 栈

栈是一种线性数据结构，遵循后进先出（LIFO）原则。栈的基本操作包括入栈（push）、出栈（pop）和查看栈顶元素（peek）。

```python name=stack.py
class Stack:
    def __init__(self):
        self.items = []

    def push(self, item):
        self.items.append(item)

    def pop(self):
        if not self.is_empty():
            return self.items.pop()
        return None

    def is_empty(self):
        return len(self.items) == 0

    def peek(self):
        if not self.is_empty():
            return self.items[-1]
        return None

# 示例
stack = Stack()
stack.push(10)
stack.push(20)
stack.push(30)
print(stack.pop())  # 输出 30
print(stack.peek())  # 输出 20
```

### 队列

队列是一种线性数据结构，遵循先进先出（FIFO）原则。队列的基本操作包括入队（enqueue）和出队（dequeue）。

```python name=queue.py
class Queue:
    def __init__(self):
        self.items = []

    def enqueue(self, item):
        self.items.append(item)

    def dequeue(self):
        if not self.is_empty():
            return self.items.pop(0)
        return None

    def is_empty(self):
        return len(self.items) == 0

# 示例
queue = Queue()
queue.enqueue(10)
queue.enqueue(20)
queue.enqueue(30)
print(queue.dequeue())  # 输出 10
print(queue.dequeue())  # 输出 20
```
