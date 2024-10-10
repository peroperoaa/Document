# UE5 Delay方法不执行

> 在UE5中，使用Delay节点的蓝图可能不会按预期执行。这个问题可能会导致游戏逻辑出现异常，影响游戏的正常运行。

#### 原因分析：

[开发者社区](https://forums.unrealengine.com/t/why-does-delay-not-work/444588/1)给出的原因：

> Whatever you do after you destroy the actor will not be called as you already destroyed the caller (Delay node will not make the Actor stick around).
>
> 翻译：一旦Actor被销毁,之后对它的任何操作都不会被执行。即使使用延迟节点(Delay node)也无法让Actor继续存在。

#### 解决方案：

一个可参考的解决方案是使用`SetActorHiddenInGame`方法，通过隐藏Actor来暂时延缓销毁Actor，实现Delay节点的执行。

1. 在原来调用`DestroyActor`方法的地方，替换成`SetActorHiddenInGame`，并将`NewHidden`选项勾上(隐藏Actor及其所有组件)。
2. 在确定`Delay`节点执行完(包括后继想要执行的节点完成)之后在执行`DestroyActor`方法。