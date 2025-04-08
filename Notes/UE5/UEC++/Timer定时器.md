# UE5 C++ 定时器系统

## 概述
定时器是游戏引擎必须提供的基础功能之一，不仅常见于游戏开发中，在其他程序开发中亦频繁出现。定时器能够在约定的时间以约定的频率执行某函数，常用于查询某条件是否成立、轮询是否收到答复、定时处理消息等。

UE5提供了SetTimer作为设置定时器的简便方法，本文将详细介绍其用法。

## 定时器的基本用法

### 设置定时器
定时器的设置只需三步即可完成：

1. 声明定时器句柄 FTimerHandle
2. 定义执行函数
3. 设置定时器

#### 声明FTimerHandle
首先是在类定义中声明定时器句柄：

```cpp
UCLASS()
class GOD_API ACylindricalWall : public AActor
{
    // ...existing code...
private:
    // ...existing code...
    FTimerHandle MonitorTimer;
};
```

#### 定义执行函数
定义一个将由定时器定时执行的函数：

```cpp
void ACylindricalWall::MonitorPlayer()
{
    auto Now = FDateTime::Now();
    UE_LOG(LogTemp, Warning, TEXT("MonitorPlayer Time:%d %d %d"), 
           Now.GetMinute(), Now.GetSecond(), Now.GetMillisecond());
    
    auto Player = Cast<AGodCharacter>(UGameplayStatics::GetPlayerPawn(GetWorld(), 0));
    if (Player != NULL)
    {
        bool bNotVisible = (GetSquaredDistanceTo(Player) <= 30000);
        SetActorHiddenInGame(bNotVisible);
    }
}
```

#### 设置定时器
调用以下语句设置定时器：

```cpp
GetWorld()->GetTimerManager().SetTimer(MonitorTimer, this, &ACylindricalWall::MonitorPlayer, 1, true, 2);
```

通常这条语句可在Actor的BeginPlay()函数中调用。

SetTimer函数的参数解析：

- **InOutHandle**: 定时器绑定的句柄，如果该句柄已指向其他定时器，则取消这个其他定时器
- **InObj**: 调用执行函数的对象
- **InTimerMethod**: 定时器所执行的函数
- **InRate**: 函数执行的时间间隔(秒)，如果<=0，则清除现存定时器
- **InbLoop**: 该定时器是否循环，若不循环则只执行一次
- **InFirstDelay**: 从设置定时器到执行定时器的时间间隔，若<0，则使用InRate代替
- **注**: 当不设置循环时，延迟默认调用InFirstDelay,当<0，时才使用InRate。
### 清除定时器
设置定时器后，一定要记得在适当的时机清除定时器：

```cpp
GetWorld()->GetTimerManager().ClearTimer(MonitorTimer);
```

通常可以在Actor的EndPlay()函数中执行清除操作。

## 定时器的三种模式

### 延迟模式
在设置定时器后的一段时间后执行某函数一次：

```cpp
// 延迟2秒后执行MonitorPlayer()函数一次
GetWorld()->GetTimerManager().SetTimer(MonitorTimer, this, &ACylindricalWall::MonitorPlayer, 1, false, 2);
```

### 循环模式
设置定时器后立即开始每隔一段时间执行函数，直到定时器被清除：

```cpp
// 立即开始，每隔1秒执行MonitorPlayer()函数
GetWorld()->GetTimerManager().SetTimer(MonitorTimer, this, &ACylindricalWall::MonitorPlayer, 1, true, 0);
```

### 延迟循环模式
设置定时器后延迟一段时间开始第一次执行，然后每隔一段时间执行一次函数：

```cpp
// 延迟2秒后第一次执行，之后每隔1秒执行MonitorPlayer()函数
GetWorld()->GetTimerManager().SetTimer(MonitorTimer, this, &ACylindricalWall::MonitorPlayer, 1, true, 2);
```

## 执行函数的选择

### 以类的成员函数为执行函数
如前面的例子所示，可以使用类的成员函数作为定时器的执行函数。

### 以Lambda为执行函数
Lambda函数也可以作为执行函数：

```cpp
auto MonitorLambda = [this]()
{
    auto Now = FDateTime::Now();
    UE_LOG(LogTemp, Warning, TEXT("MonitorPlayer Time:%d %d %d"), 
           Now.GetMinute(), Now.GetSecond(), Now.GetMillisecond());
    
    auto Player = Cast<AGodCharacter>(UGameplayStatics::GetPlayerPawn(GetWorld(), 0));
    if (Player != NULL)
    {
        bool bNotVisible = (GetSquaredDistanceTo(Player) <= 30000);
        SetActorHiddenInGame(bNotVisible);
    }
};

GetWorld()->GetTimerManager().SetTimer(MonitorTimer, MonitorLambda, 1, true, 2);
```

## 使用定时器的易错点

### 易错点一：在Actor的构造函数中设置定时器
- **错误**：在Actor的构造函数中设置定时器。
- **原因**：此时Actor还没有完全Spawned出来。
- **正确做法**：在Actor的BeginPlay()函数中设置定时器。

### 易错点二：在延迟模式下，设置SetTimer参数InRate为0
- **错误**：在延迟模式下将InRate参数设为0。
- **原因**：当InRate <= 0时，会清除现有定时器，导致函数不会执行。
- **正确做法**：即使在延迟模式下，也要将InRate设置为一个大于0的值。