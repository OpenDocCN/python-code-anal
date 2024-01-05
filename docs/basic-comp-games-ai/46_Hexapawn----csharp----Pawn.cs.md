# `46_Hexapawn\csharp\Pawn.cs`

```
namespace Hexapawn;

// 表示棋盘上一个单元格的内容
internal class Pawn
{
    // 表示黑色棋子的静态实例
    public static readonly Pawn Black = new('X');
    // 表示白色棋子的静态实例
    public static readonly Pawn White = new('O');
    // 表示空单元格的静态实例
    public static readonly Pawn None = new('.');

    // 棋子的符号
    private readonly char _symbol;

    // 私有构造函数，用于创建棋子实例
    private Pawn(char symbol)
    {
        _symbol = symbol;
    }

    // 重写 ToString 方法，返回棋子的符号
    public override string ToString() => _symbol.ToString();
}
```