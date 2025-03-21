# UE常用变量类型

## 基础类型
```cpp
// 布尔类型（true/false）
bool varBool; 

// 32位整数（范围约±21亿）
int32 varInt32;

// 64位整数（超大整数范围）
int64 varInt64;

// 字节类型（0-255的无符号整数）
BYTE varByte;
```

## 字符串类型
```cpp
// 可变字符串（类似std::string，支持动态修改）
FString varString = TEXT("Hello World");

// 不可变名称标识（用于资源路径等，内存效率高）
FName MyName = FName(*MyString);

// 本地化文本
FText MyText = FText::FromString(MyString);
```

## 数学相关类型
```cpp
// 三维坐标（X/Y/Z轴位置）
FVector varVector(1.0f, 2.0f, 3.0f);

// 三维旋转（Pitch俯仰/X, Yaw偏航/Z, Roll滚转/Y）
FRotator varRotator(0.0f, 90.0f, 0.0f);

// 变换矩阵（包含位置+旋转+缩放）
FTransform varTransform;
/* 
包含:
- Location（位置向量）
- Rotation（旋转四元数）
- Scale3D（缩放比例）
*/
```

> **理解**：
>
> 1. `FVector`就像游戏中的GPS坐标(X,Y,Z确定位置)
> 2. `FRotator`类似相机云台的三个旋转轴控制
> 3. `FTransform`相当于一个物体的完整身份证（在哪+怎么转+有多大）
> 4. `FName`适合存储不会改变的标识（如资源路径）
> 5. `FText`专门处理需要翻译的文本