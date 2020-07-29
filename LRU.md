# LRU算法

缓存淘汰策略

双向链表 + 哈希表实现

双向链表

```python
class Node():
    def __init__(self, key=None, val=None):
        self.key = key
        self.val = val
        self.next = None
        self.pre = None

class DoubleList():
    def __init__(self, key=None, val=None):
        self.head = Node(key, val)

    # 添加x节点到表头
    def addFirst(x):
        x.next = self.head
        self.head.pre = x
        self.head = x

    # 删除x节点
    def remove(x):
        x.pre.next = x.next.next
        x.next.pre = x.pre
        x.next = None
        x.pre = None

    # 删除最后一个节点
    def removeLast():
        node = self.head
        while node.next:
            node = node.next
        node.pre.next = None
        node.pre = None
        return node
    
    # 返回链表的长度
    def size():
        node = self.head
        n = 0
        while node:
            n += 1
            node = node.next
        return n
```

```python
class LRUcache():
    def __init__(self, cap=3):
        self.map = {}
        self.cache = DoubleList()
        self.cap = cap
    
    def get(key):
        if key not in self.map: return -1
        val = self.map[key].val
        self.put(key, val)
        return val
    
    def put(key, val):
        x = Node(key, val)

        if key in self.map:
            self.cache.remove(self.map[key])
            self.cache.addFirst(x)
            self.map[key] = x
        else:
            if self.cap == self.cache.size():
                last = self.cache.removeLast()
                self.map.pop(last.key)
            self.cache.addFirst(x)
            self.map[key] = x
```