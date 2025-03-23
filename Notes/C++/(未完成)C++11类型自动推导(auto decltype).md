# C++ 自动类型推导：`auto` 与 `decltype`

---

#### **1. `auto`：让编译器推导变量类型**
待施工

---

#### **2. `decltype`：精确获取表达式类型**
- **基本规则**：  
  
- 第一步，若无括号则返回expr类型
  
- 第二步，若是函数调用返回函数返回类型

- 第三步，若有括号则返回类型引用

- 第四步，返回expr类型

  ```cpp
  int a = 10;
  const int& ref = a;
  
  decltype(ref) b = a;   // b 的类型是 const int&
  decltype(a + 1) c = a; // c 的类型是 int（a+1 是右值）
  decltype(a) b = a;    // b 的类型是 int
  decltype((a)) c = a;  // c 的类型是 int&（括号使表达式变为左值）
  ```

- **使用场景**： 
  
  - 结合后置返回类型声明函数返回值（C++11）。//auto为占位符，类型有->后面决定
  ```cpp
  template<typename T1, typename T2>
  auto add(T1 a, T2 b) -> decltype(a + b) {
      return a + b; // 返回类型由 a + b 的结果类型决定
  }
  ```

---

#### **3. `auto` vs `decltype`：关键区别**
| 特性           | `auto`                         | `decltype`                   |
| -------------- | ------------------------------ | ---------------------------- |
| 推导目标       | 根据初始化表达式推导变量类型   | 根据表达式推导类型（不赋值） |
| 引用处理       | 默认忽略引用，需显式写 `auto&` | 保留引用的原始类型           |
| `const` 处理   | 默认忽略顶层 `const`           | 保留 `const` 和底层 `const`  |
| 表达式类型推导 | 不支持（仅用于变量初始化）     | 支持任意表达式               |

