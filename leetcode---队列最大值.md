```python
请定义一个队列并实现函数 max_value 得到队列里的最大值，要求函数max_value、push_back 和 pop_front 的均摊时间复杂度都是O(1)。

若队列为空，pop_front 和 max_value 需要返回 -1

示例 1：

输入: 
["MaxQueue","push_back","push_back","max_value","pop_front","max_value"]
[[],[1],[2],[],[],[]]
输出: [null,null,null,2,1,2]
示例 2：

输入: 
["MaxQueue","pop_front","max_value"]
[[],[],[]]
输出: [null,-1,-1]
```

代码及其注释
```python
import queue

class MaxQueue:

    def __init__(self):
        self.queue = queue.Queue()
        self.deque = queue.deque()  # 递减队列


    def max_value(self) -> int:
        # 直接返回deque首项
        return self.deque[0] if self.deque else -1


    def push_back(self, value: int) -> None:
        self.queue.put(value)
        # while循环把比新值更低的值全删掉
        while self.deque and self.deque[-1] < value:
            self.deque.pop()
        self.deque.append(value)


    def pop_front(self) -> int:
        if self.queue.empty():
            return -1
        else:
            val = self.queue.get()  # get返回queue首项后便除去首项了
            # 控制deque首项相同，才可作为queue的最大值
            if self.deque[0]==val:
                self.deque.popleft()
            return val


```
[解题思路](https://leetcode.cn/leetbook/read/illustration-of-algorithm/e2tfiv/)
