# `basic-computer-games\33_Dice\csharp\Program.cs`

```

// 命名空间 BasicComputerGames.Dice
namespace BasicComputerGames.Dice
{
    // 定义一个名为 Program 的类
    public class Program
    {
        // 程序的入口点
        public static void Main(string[] args)
        {
            // 创建一个 Game 类的实例
            Game game = new Game();

            // 调用 GameLoop 函数，这将在循环中无限地玩游戏，直到玩家选择退出
            game.GameLoop();
        }
    }
}

```