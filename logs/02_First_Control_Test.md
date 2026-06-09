# 02_First_Control_Test.md
## 关节物理与键盘控制
导入成功后的第一次运行
>
> SO-101 URDF 成功导入 Unity 后，我决定先运行场景，看看机械臂是否能够正常工作。结果 Console 里立刻出现了报错：当前项目使用的是新的 Input System，但 URDF Importer 中的控制脚本仍在调用旧版 `UnityEngine.Input`。
>
> 这个报错可太经典了，经常遇到，我立马意识到 Unity 输入系统的新旧版本冲突，需要进一步调整 Player Settings 或脚本兼容性。同时，这个报错也说明导入的机械臂文件中并不是一个完全静态的模型，它本身已经包含了一个通过键盘控制的现成脚本。对我来说，这反而是一个好消息。\
<img width="2056" height="431" alt="image" src="https://github.com/user-attachments/assets/cb39ec1f-b856-4750-93d8-1232c4890daf" />

<br><br><br>
运行后整个机械臂开始下坠，我怀疑是重力影响
<img width="1431" height="810" alt="image" src="https://github.com/user-attachments/assets/9ce6d9cb-a2ee-463b-8459-e4a24b2713ba" />

<br><br><br>
在其自带组件中发现管理所有刚体重力的开关
<div align="center">
<img width="486" height="453" alt="image" src="https://github.com/user-attachments/assets/74e4f735-6566-40f8-b4b9-d0a411a37e35" />
</div>
下坠问题解决，但是我们过一下还会回来再次解决这个问题

<br><br><br>

> 在关闭重力之后，机械臂不再受到下坠影响。由于只有关节运动而没有重量反馈，整个运动状态看起来非常奇怪。
>
> 它既有点像失重环境中的机械臂，又有点像一条在太空舱里缓慢蠕动的蛆。
>
> 没想到重力对于机器人运动的观感影响有这么大。
>
> 人对于“机械臂应该如何运动”的理解，其实很大程度上来自现实世界中的重力经验。

https://github.com/user-attachments/assets/78c6b0ca-e5f9-4a46-8706-dacc7b28dea0

拓展议题
> Embodied cognition（具身认知）
> 
> Gravity as an invisible design material（重力作为一种不可见的设计材料）
> 
> 为什么失重环境中的运动会让人产生“生物感”

> Space Worm Robot（太空蛆机械臂）

<br><br><br>

 在进一步探索中，我发现每一个关节的组件里都有一个名为 `Immovable` 的开关。

> 如果只希望机械臂的底座固定在原地，而不是像之前那样整体漂浮或滑动，就可以将底座关节上的 `Immovable` 打开。
>
> 打开之后，底座能够稳定地固定在场景中，而上方的机械臂部分仍然可以继续进行关节运动。这样一来，机械臂的行为就更接近现实中的固定安装状态。
<div align="center">
<img width="507" height="464" alt="image" src="https://github.com/user-attachments/assets/18a568be-3b19-4610-903e-997c4f27bb5a" />
</div>

在调整 `Controller` 脚本之后，虚拟机械臂终于可以通过键盘进行控制。

> 不过，虽然机械臂已经能够正常运动，但其实此时我对整个系统内部的工作方式仍然非常模糊。

https://github.com/user-attachments/assets/6058375b-3c02-4240-bce2-7c7f6be521ec

> 导入后的机械臂自带了大量脚本，而我并不清楚它们之间的关系和分工。根据目前的观察，真正频繁接触到的主要有：
>
> - `URDFRobot`
> - `Controller`
>
> 剩下的目前还不需要做任何调整暂未接触
> - `FKRobot`
> - `UrdfPlugin`
> - `UrdfVisual`
> - `UrdfCollision`
>
> 其中，`Controller` 负责键盘控制，而其它脚本的作用当时仍然完全不清楚。我知道它们一定在整个机器人系统中承担着不同的职责，但对于它们如何协同工作、谁负责运动、谁负责显示、谁负责碰撞，我都还没有建立起完整的理解。
>
> 虽然机械臂已经开始“活”了起来，但我对于支撑它运行的内部结构仍然几乎一无所知。


