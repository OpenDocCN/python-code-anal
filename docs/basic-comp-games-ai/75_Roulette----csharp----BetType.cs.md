# `basic-computer-games\75_Roulette\csharp\BetType.cs`

```

namespace Roulette; // 命名空间声明，定义了代码所在的命名空间

internal record struct BetType(int Value) // 定义了一个内部的记录结构体 BetType，包含一个整数类型的属性 Value
{
    public static implicit operator BetType(int value) => new(value); // 定义了一个隐式转换操作符，将整数类型转换为 BetType 类型

    public int Payout => Value switch // 定义了一个只读属性 Payout，根据 Value 的值返回不同的赔率
        {
            <= 36 or >= 49 => 35, // 当 Value 小于等于 36 或大于等于 49 时，返回 35
            <= 42 => 2, // 当 Value 小于等于 42 时，返回 2
            <= 48 => 1 // 当 Value 小于等于 48 时，返回 1
        };
}

```