# 03_Connecting_the_Physical_and_Virtual_Robot.md
## digital twin
> 在开始构建数字孪生时，我也考虑过使用 ROS 作为实体机械臂与 Unity 之间的通信桥梁。毕竟在机器人领域，ROS 几乎是一种标准方案。
>
> 但最终我没有选择 ROS，而是自己编写了简单的通信脚本。
>
> 最主要的原因是，我当前的目标并不是构建一个复杂的机器人系统，而只是实现实体机械臂与虚拟机械臂之间的状态同步。对于这个目标来说，ROS 所提供的大量功能实际上超出了现阶段的需求。

数字孪生 = 实体系统 + 虚拟系统 + 实时数据连接/交换

说实话，这里我没搞懂怎么回事，虽然我回去跟着重复做了一边但仍然不知道是如何解决的

<dv><dv><dv>

https://github.com/user-attachments/assets/e14435af-1489-4e2f-8710-a737c7c72bf6

<div align="right">
<sub><i>Video 1. Initialization failed to synchronize.</i></sub>
</div>

<dv><dv><dv>

[数字孪生架构与同步问题说明.pdf](https://github.com/user-attachments/files/28775026/default.pdf)

实在没招了，让claude把对话过程中重要的内容总结成文档形式了

<dv><dv><dv>

https://github.com/user-attachments/assets/6203a28a-9795-44e4-9f6c-62c6217aa0bc

<div align="right">
<sub><i>Video 2. Synchronization successful.</i></sub>
</div>


