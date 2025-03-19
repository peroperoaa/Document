# UE 日志与屏幕调试信息

## 目录
1. [日志基础](#日志基础)
2. [屏幕调试信息](#屏幕调试信息)
3. [代码示例](#代码示例)

---

## 日志基础
### 日志级别（重要程度排序）
| 级别    | 颜色   | 说明                   |
| ------- | ------ | ---------------------- |
| Error   | 🔴 红色 | 严重错误，需要立即处理 |
| Warning | 🟡 黄色 | 警告，需要注意的问题   |
| Display | ⚪ 白色 | 普通调试信息           |

### UE_LOG 基本用法
```cpp
// 格式：UE_LOG(分类, 级别, 内容)
UE_LOG(LogTemp, Error, TEXT("错误信息"));   	// 红色错误
UE_LOG(LogTemp, Warning, TEXT("警告信息"));		// 黄色警告
UE_LOG(LogTemp, Display, TEXT("普通信息"));		// 白色信息
```

---

## 屏幕调试信息
### 直接显示到游戏画面
```cpp
// 格式：AddOnScreenDebugMessage(参数1, 参数2, 参数3, 参数4)
GEngine->AddOnScreenDebugMessage(
    -1,             // 参数1：-1=不覆盖之前消息
    5.0f,           // 参数2：显示时间
    FColor::Red,    // 参数3：显示颜色
    TEXT("显示内容") // 参数4：要显示的文字
);
```

---

## 代码示例
### 完整示例代码
```cpp
// 日志记录示例
UE_LOG(LogTemp, Error, TEXT("角色血量过低！")); 
UE_LOG(LogTemp, Warning, TEXT("弹药不足警告"));
UE_LOG(LogTemp, Display, TEXT("进入新区域"));

// 屏幕显示示例
GEngine->AddOnScreenDebugMessage(-1, 3.0f, FColor::Green, TEXT("任务完成！"));
GEngine->AddOnScreenDebugMessage(-1, 2.5f, FColor::Yellow, TEXT("获得金币+50"));
```

