# 指针 & const

## 常量指针 & 指针常量

### 常量指针（指向常量的指针）
```cpp
const int* p = &a;
```

- 不能通过 `p` 修改 `a`，包括 `*(p + 1)`, `*(p + 2)` 等操作

### 指针常量（指针本身是常量）
```cpp
int* const p = &b;
```
- 不能修改 `p` 的指向

---

## 转换规则（const/non-const 指针）

| 类型               | 说明                                                         |
| ------------------ | ------------------------------------------------------------ |
| 非const -> 非const | 允许                                                         |
| const -> 非const   | 当且仅当非const与const之间仅有一层间接关系时（如指向基本数据类型）允许 |
| 非const -> const   | 不允许（通过非const指针修改const值很荒谬）                   |
| const -> const     | 允许                                                         |

### 补充说明
1. `const -> 非const` 转换需要显式强制类型转换（例如使用 `const_cast`）
2. `非const -> const` 转换是隐式允许的（可以增强访问安全性）
3. 多层间接关系（如 `int**` 到 `const int**`）的转换存在限制

