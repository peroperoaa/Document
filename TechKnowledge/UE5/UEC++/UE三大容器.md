# UE 基础容器操作指南（TArray, TSet, TMap）

## 1. TArray（动态数组）

### 特性

- 有序集合，支持快速随机访问
- 允许重复元素
- 内存连续，适合频繁遍历

### 常用操作

#### **增**

```CPP
TArray<int32> MyArray;

// 添加元素到末尾
MyArray.Add(10); 

// 原地构造元素（避免拷贝）
MyArray.Emplace(20); 

//如果没有20则添加到末尾
MyArray.AddUnique(20);

// 插入到指定位置（索引1）
MyArray.Insert(5, 1); 
```

#### **删**

```cpp
// 删除所有的元素
MyArray.Remove(10); 

//删除数组中第一个与 10 相同的元素
MyArray.RemoveSingle(10);

// 删除指定索引元素（后续元素前移）
MyArray.RemoveAt(0); 

// 重置数组为0
MyArray.Reset(); 

// 清空数组
MyArray.Empty(); 
```

#### **改**

```CPP
// 直接修改索引元素
MyArray[0] = 100; 
```

#### **查**

```CPP
// 查找元素（返回索引，找不到返回INDEX_NONE）
int32 Index = MyArray.Find(20); 

//反向查找第一个匹配的元素，返回下标
int32 Index = MyArray.FindLast(10);

// 检查某个值是否存在
bool bExists = MyArray.Contains(5); 
```

------

## 2. TSet（无序集合）

### 特性

- 无序唯一元素集合
- 基于哈希表，查找效率 O(1)
- 不支持重复元素

### 常用操作

#### **增**

```CPP
TSet<FString> MySet;

// 添加元素（若存在则忽略）
MySet.Add(TEXT("Banana"));
MySet.Add(TExT("Grapefruit"));
MySet.Add(TEXT("Pineapp1e"));

// 原地构造（推荐）
MySet.Emplace（TEXT（"Orange"));

//合并元素
TSet<FString>MySet2;
MySet2.Add（TEXT("zhangsan"))
MySet2.Add(TEXT("1isi"));
MySet2.Add(TEXT("wangwu"));

//Append将Myset2合并到Myset中
MySet.Append（MySet2);
```

#### **删**

```CPP
// 删除元素（返回删除数量，不存在则为0）
int32 RemovedCount = MySet.Remove(TEXT("Apple")); 

//清空容器但保留内存
MySet.Reset();

// 清空集合
MySet.Empty(); 
```

#### **查**

```CPP
// 检查存在性
bool bExists = MySet.Contains(TEXT("Banana")); 

//num函数是查询集合中保存的元素数量
int32Count = MySet.Num();

//返回指向元素数值的指针，如果映射不包含该键，则返回Null
FString* isFind2 = MySet.Find（TEXT（"Banan"））;
```

#### **其他**

```CPP
//函数会返回—个Tarray，其中填充了TSet中每一个元素的副本
TArray<FString>FruitArray = MySet.Array();

//排序
TSet<FString>TestSet ={TEXT("a"),TEXT("aa"),TEXT("aaa"),TEXT("aaaa")};
TestSet.Sort（[](FString A,FString B) {return A.Len() >B.Len());
                                      
//[]FSetElementID访问集合对应元素的引|用
FSetE1ementId Index = NewSet.Add(TEXT("Twotwo"));
TestSet[Index] = TEXT("One"）;
                      
//ReServe
TSet<FString>NewSet1;
NewSet1.Reserve(10);//预先分配内存，若输入的Number大于元素的个数，则会产生闲置内存(Slack)
                      
//Shrink
for（int32 i = 0; i < 10; i++)
	NewSet1.Add(FString::Printf(TEXT("NewSet%d"),i));//添元素
for（int32 i = 0; i < 10; i += 2)
	NewSet1.Remove(FSetElementId::FromInteger（i));//册除元素产生闲置内存
NewSet1.Shrink();//删除末端的空元素
//Compact将容器中的所有空白的元素集合到一起放到末尾一起删除
NewSet1.Compact()：//注意Compact可能会改变元素之间的顺序，如果不想改变顺序，可以使用CompactStable
NewSet1. Shrink();
```



------

## 3. TMap（键值对）

### 特性

- 无序键值对集合
- 键唯一，基于哈希表
- 快速查找（O(1)）

### 常用操作

#### **增**

```CPP
TMap<FString, int32> MyMap;

// 添加键值对（若键存在则覆盖）
MyMap.Add(TEXT("Apple"), 5); 

// 原地构造（推荐）
MyMap.Emplace(TEXT("Banana"), 10); 
```

#### **删**

```CPP
// 通过键删除
MyMap.Remove(TEXT("Apple")); 

// 清空字典
MyMap.Empty(); 
```

#### **改**

```CPP
// 直接修改值
MyMap[TEXT("Banana")] = 20; 
```

#### **查**

```CPP
// 通过键访问值（不存在会触发断言）
int32 Val = MyMap[TEXT("Banana")]; 

// 检查键是否存在，返回指针
int32* Pointer = MyMap.Find("Apple");

// 检查值是否存在，返回指针
int32* Pointer = MyMap.FindKey(10);

// 检查键是否存在，返回bool值
bool bExists = MyMap.Contains(TEXT("Apple")); 

// 获得key和value数组
TArray<FString> Keys;
MyMap.GenerateKeyArray(Keys);
TArray<int32> Values;
MyMap.GenerateValueArray(Values);
```