# `basic-computer-games\83_Stock_Market\csharp\Assets.cs`

```

// 引入不可变集合的命名空间
using System.Collections.Immutable;

// 定义游戏命名空间
namespace Game
{
    /// <summary>
    /// 存储玩家的资产。
    /// </summary>
    // 定义资产记录
    public record Assets
    {
        /// <summary>
        /// 获取玩家现金金额。
        /// </summary>
        // 获取或初始化现金属性
        public double Cash { get; init; }

        /// <summary>
        /// 获取每家公司拥有的股票数量。
        /// </summary>
        // 获取或初始化不可变整数数组属性
        public ImmutableArray<int> Portfolio { get; init; }
    }
}

```