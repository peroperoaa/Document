# 用数组(vector)模拟栈

   ##  1. **前置工作**

```cpp
int stk[N];
top = 0;
```

## **2. 函数** 

push: stk[++top] = x;

pop: --top;

sise: top;

empty: top == 0;

top: stk[top - 1];