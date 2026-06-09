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

<br><br><br><br>
在其自带组件中发现管理所有刚体重力的开关

<img width="486" height="453" alt="image" src="https://github.com/user-attachments/assets/74e4f735-6566-40f8-b4b9-d0a411a37e35" />

下坠问题解决，但是我们过一下还会回来再次解决这个问题


