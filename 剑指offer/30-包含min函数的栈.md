### 30-包含min函数的栈

​	题目描述

> 定义栈的数据结构，请在该类型中实现一个能够得到栈的最小元素的 min 函数在该栈中，调用 min、push 及 pop 的时间复杂度都是 O(1)。

​	示例

```java
MinStack minStack = new MinStack();
minStack.push(-2);
minStack.push(0);
minStack.push(-3);
minStack.min();   --> 返回 -3.
minStack.pop();
minStack.top();      --> 返回 0.
minStack.min();   --> 返回 -2.
```

​	提示

1. 各函数的调用总次数不超过 20000 次、

### 1：辅助栈

- 此题的意思：在时间复杂度为`O(1)`的情况下找出此栈中的最小值
- 那么我们可以创建一个只存储最小值的辅助栈
- `push()`：判断辅助栈是否为空，为空情况：直接压入栈；不为空情况：比较此时压入的值与辅助栈栈顶元素的大小，`x<stack.peek():压入栈`
- `pop()`：判断栈与辅助栈栈顶元素是否相等。`stack1.peek()==stack2.peek()`：两个栈都弹出栈顶
- `min()`：返回辅助栈的栈顶
- `top()`：返回栈的栈顶

```java
class MinStack {
    Stack<Integer> stack1;
    Stack<Integer> stack2; //辅助栈（最小栈）

    /** initialize your data structure here. */
    public MinStack() {
        stack1 = new Stack<>();
        stack2 = new Stack<>();
    }
    
    public void push(int x) {
        stack1.push(x);
        if(stack2.isEmpty()) {
            stack2.push(x);
        } else {
            if(x < stack2.peek()) {
                stack2.push(x);
            }
        }
    }
    
    public void pop() {
        if(stack1.peek() == stack2.peek()) stack2.pop(); 
        stack1.pop();
    }
    
    public int top() {
        return stack1.peek();
    }
    
    public int min() {
        return stack2.peek();
    }
}
```

> 时间复杂度：`O(1)`，空间复杂度：`O(n)`