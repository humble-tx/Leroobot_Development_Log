## 选择unity作为Robotics Simulation Platform
手头的设备使用的是3060的显卡
结合现有的硬件条件、知识基础和研究目标，Unity虽然再各方面无法比肩issac sam但确是目前最合适的平台。

## 将 SO-101 URDF 导入 Unity
最开始是我想的很简单，只需要把带有关节信息的模型文件导入unity就完成了。没想到这一步却异常困难。\
### 参考LLM的推荐，使用URDF Importer 0.5.2-preview插件\
<img width="1817" height="844" alt="image" src="https://github.com/user-attachments/assets/e0ca8bed-9955-4f73-b645-dc23f1083987" />


### 并将开源模型文档导入到project>assets文件夹中\
<img width="1625" height="587" alt="image" src="https://github.com/user-attachments/assets/96e6c49c-7a0b-424d-9d12-2e0e74e057e5" />


选择对应urdf模型文件右键点击Import Robot from Selected URDF file
<div align="center">
<img width="50%" alt="屏幕截图 2026-06-09 150909" src="https://github.com/user-attachments/assets/75245928-0f4e-4ba2-ace5-fd704cd1a6d7" />
</div>


后弹出下图内容，将Mesh Decomposer调制unity模式以减小模型碰撞体积细节和碎片文件，减轻cpu负担
<div align="center">
  <img width="752" height="340" alt="image" src="https://github.com/user-attachments/assets/afa68618-b7db-407f-9798-cfa5c576684d" />
</div>


#### 但是问题就出在这里!!! 导入后不显示模型,由于完全不懂只能求助AI，由此展开了第一轮的Iterative Debugging（迭代式调试）
按照调试的先后顺序大致分为四次不同的尝试，最后一次最复杂也最烦人
- 先给出的建议是点击 so101_new_calib 按 F 键对焦——但是相机飞过去仍然看不见东西
- claude进一步让我展开 Hierarchy 层级查看子对象——发现层级结构是有的

-n发现底部console报错说模型未加载好
<img width="2559" height="1520" alt="image" src="https://github.com/user-attachments/assets/c9bdb5c4-a394-4dd4-9f06-36a0fe769631" />
但并未发现未加载好的情况于是删掉空白object重新导入，

- 点进最深层的子对象看 Inspector——发现 Mesh Filter 里 mesh 和material是空的
>这个结论的得出非常的折腾，最主要的问题是我完全不动导入Hierarchy里的文件结构和功能，可以从下面的一个分支的展开结构感受到这个开源模型文档的复杂程度
<div align="center">
<img width="611" height="845" alt="image" src="https://github.com/user-attachments/assets/4651a3bf-af0f-4121-8aaa-b72fa7a3e386" />
</div>

按照claude给出的步骤，我开始检查导入 Unity 后的模型文件本身是否存在问题。
按要求将prefab文件拖入后，也没有显现内容，
> 这里其实开始怀疑是不是模型文件本身出了问题。但我的制作顺序是先利用这些文件成功打印出了实体机械臂，再开始制作数字孪生。既然实体能够正常打印，理论上说明模型文件本身应该没有问题。然而在 Unity 中，甚至连单个模型都无法正常显示，这让我始终无法理解问题出在哪里。
>
> 于是我只能暂时跳过这个疑问，转而去检查整个 Hierarchy 的文件结构。但实际上，此时的我仍然完全不知道整个项目的结构是怎样组织的。

转向对整体的检查：
> 由于 Claude 也不知道这个文件内部的具体结构是什么样的，它能看到的其实只有 Hierarchy 里面最外层的结构。比如它能看到某个对象前面有一个可以下拉的箭头，于是它知道下面应该还有一个层级，但它并不知道这个层级下面还有多少东西，也不知道真正需要找的组件到底藏在哪。
>
> 所以最开始，它让我去第一个层级截图，看有没有它需要的组件。我截给它，它说没有；然后让我再往下一层找，还是没有。就这样一层一层地往下。
>
> 但问题是，我其实完全不知道它在找什么。
>
> 它最开始只是说要找一个 Mesh 的东西，但我根本不知道这个东西是干什么用的，也不知道它会以什么形式存在。因为在我看来，里面大部分都是 Script、Transform 之类的组件，我根本不知道它是不是藏在某个脚本里面，或者是不是我已经看到了但自己没有意识到。
>
> 所以它所说的东西对我来说一直都是很模糊的。我能做的只有按照它的要求，一层一层地去筛选。截图、发送、等待回复；再截图、再发送、再等待回复。
>
> 一直筛到最后一层，它终于在右侧 Inspector 里看到了它想找的东西，但发现这个组件是空的。到这里，问题终于找到了。
>
> 但是整个搜索过程，以及应该如何提问、为什么要这样找，我始终都是模糊的。我并没有真正理解发生了什么，只是在机械地重复

这就是问题所在\
<img width="2557" height="1529" alt="屏幕截图 2026-06-09 154009" src="https://github.com/user-attachments/assets/7301ce8f-df04-48dc-a4ef-be10425be418" />
<div align="center">
<img width="509" height="236" alt="image" src="https://github.com/user-attachments/assets/3cfc92f0-4d96-47f2-a887-74bb6273ecac" />
</div>

由此对整个结构有所了解后，反过来对单个模型精选研究\
> 这里最让我困惑的是，我一开始并不清楚自己导入 Unity 的到底算是 STL 模型，还是 URDF 结构。它并不是我原本想象的那种“一个零件对应一个 STL 文件”的简单关系。相反，每一个机械臂零件在 Unity 里又被拆分成了好几种文件类型。

从 Project 面板里看，每个模型大概会对应四类文件：

1. 一个像普通文件页面一样的图标，后缀是 `.part`；

2. 一个粉色的、带有大致形体轮廓的 `.prefab` 预制件；

3. 一个 `.stl` 文件，但因为我电脑里 STL 被 Bambu Studio 关联了，所以图标显示成了 Bambu Studio 的样子；

4. 一个或两个带网格图标的 `.asset` 文件。
<img width="2250" height="768" alt="image" src="https://github.com/user-attachments/assets/316da2f4-efce-4fa3-bf4f-77c7faaf8d9e" />
这和原始开源文档里的结构并不一样。原始文件夹里基本只有 `.part` 和 `.stl` 文件，但导入 Unity 后，Unity 又自动生成了 prefab 和 asset 等文件。

> 也就是说，我面对的并不是一个单纯的模型文件，而是 Unity 在导入过程中重新生成的一套资源结构。每个零件都被拆成了多个 Unity 内部资源，而我最开始并不知道这些文件分别代表什么，也不知道真正影响模型显示的是哪一个。

但这里出现了问题。当我将生成的 Prefab 拖入场景后，它依然是空的。不过其下方的两个子对象中暴露出了关键线索：其中 Mesh 和 Material 都处于空状态。随后，我分别将对应的 `.asset` Mesh 文件和材质重新绑定后，模型成功显示出来，由此推断问题很可能出在这里。
<img width="2559" height="1209" alt="image" src="https://github.com/user-attachments/assets/19b9592b-af2e-468c-a6ad-7d9bd3e06d2a" />

由此Claude帮我得出了结论，mesh 文件是好的，层级结构是好的，就是两者之间的绑定缺失了

这才在claude的帮助下得出结论：mesh 文件是好的，层级结构是好的，就是两者之间的绑定缺失了

#### mesh文件绑定
> 在确认问题出现在 Mesh 引用缺失之后，我原本的想法是逐个零件手动进行绑定。检查了一下一共有25个零件之多，把这个问题再次传达给AI后，他给出了一个我看来的最优解
在之后询问claude的过程中，它将心路历程告诉了我，它发现了两个关键信息：\
>第一：25个零件，每个都是同样的问题（mesh 是空的）\
>第二：每个零件的 GameObject 名字和对应的 mesh 文件名字是一样的，比如 base_motor_holder_so101_v1 这个对象，对应的 mesh 文件就叫 base_motor_holder_so101_v1\
>这两个信息加在一起，意味着这个问题有明确的规律——不是每个零件都需要特殊处理，就是统一的"按名字找文件、填进去"。有规律的重复操作就应该用脚本，手动做25次既慢又容易出错。\
>如果零件之间没有规律，比如名字对不上、需要人工判断哪个 mesh 对应哪个对象，那脚本就很难写，手动反而更合适。

>果然机械很擅长重复的东西，但是在解决了一部分重复繁琐的任务的同时也带来了新的重复任务😭

claude帮我写好 UrdfVisualRepair.cs 脚本,我按要求放进 Assets/Editor/ 文件夹\
此时unity最上面的主菜单栏里多出了一个tools的选项, 点 Tools → Repair URDF Visuals 运行
>但是帮忙写的这个脚本也修改过很多遍,从最开始的运行后没有反应,到到Cloude给这个脚本里加了很多,debug log的语句,让我能看到console里面的反馈,但其实这个反馈对于我来说怎么样都是看不懂的,还是要把这些反馈发给Cloude,然后他再进一步的迭代。如此大概重复了两三次之后,最终它给出了一个完美绑定mesh文件的这么一个脚本出来。

脚本按名字匹配，把 25 个零件的 mesh 逐一绑上去

**"Finally, the SO-101 URDF was successfully imported into Unity."**

