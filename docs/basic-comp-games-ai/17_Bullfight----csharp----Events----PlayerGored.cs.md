# `basic-computer-games\17_Bullfight\csharp\Events\PlayerGored.cs`

```

// 在 Game.Events 命名空间下定义了一个事件记录，表示玩家被公牛顶到了。
// 该记录包含了玩家是否处于恐慌状态和是否是第一次被顶到的信息。
// 该记录被声明为 sealed，表示不可继承。
public sealed record PlayerGored(bool Panicked, bool FirstGoring) : Event;

```