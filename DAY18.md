### 155.最小栈

#### 方法1
```python
class MinStack:

    def __init__(self):
        self.stack = []
        self.min_stack = [math.inf] 

    def push(self, value: int) -> None:
        self.stack.append(value)
        self.min_stack.append(min(value,self.min_stack[-1]))

    def pop(self) -> None:
        self.stack.pop()
        self.min_stack.pop() # 为什么这里也要pop

    def top(self) -> int:
        return self.stack[-1]

    def getMin(self) -> int:
        return self.min_stack[-1]  

# Your MinStack object will be instantiated and called as such:
# obj = MinStack()
# obj.push(value)
# obj.pop()
# param_3 = obj.top()
# param_4 = obj.getMin()
```
#### 方法二，不用辅助栈
```python
class MinStack:

    def __init__(self):
        self.st = [(0,inf)]

    def push(self, value: int) -> None:
        self.st.append((value, min(self.st[-1][1], value)))

    def pop(self) -> None:
        self.st.pop()

    def top(self) -> int:
        return self.st[-1][0]

    def getMin(self) -> int:
        return self.st[-1][1]  
```

#### 方法三，差值
```python
class MinStack:

    def __init__(self):
        self.st = []
        self.mn = inf

    def push(self, value: int) -> None:
        self.st.append(value - self.mn)
        self.mn = min(self.mn, value)

    def pop(self) -> None:
        self.mn -= min(0,self.st.pop())

    def top(self) -> int:
        return self.mn + max(self.st[-1], 0)

    def getMin(self) -> int:
        return self.mn
```