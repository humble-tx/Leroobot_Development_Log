# Leroobot_Development_Log
## 选择unity作为Robotics Simulation Platform
手头的设备使用的是3060的显卡
结合现有的硬件条件、知识基础和研究目标，Unity虽然再各方面无法比肩issac sam但确是目前最合适的平台。

## 将 SO-101 URDF 导入 Unity
最开始是我想的很简单，只需要把带有关节信息的模型文件导入unity就完成了。没想到这一步却异常困难。\
参考LLM的推荐，使用URDF Importer 0.5.2-preview插件\
<img width="1817" height="844" alt="image" src="https://github.com/user-attachments/assets/e0ca8bed-9955-4f73-b645-dc23f1083987" />


并将开源模型文档导入到project>assets文件夹中\
<img width="1625" height="587" alt="image" src="https://github.com/user-attachments/assets/96e6c49c-7a0b-424d-9d12-2e0e74e057e5" />


选择对应urdf模型文件右键点击Import Robot from Selected URDF file
<div align="center">
<img width="50%" alt="屏幕截图 2026-06-09 150909" src="https://github.com/user-attachments/assets/75245928-0f4e-4ba2-ace5-fd704cd1a6d7" />
</div>


后弹出下图内容，将Mesh Decomposer调制unity模式以减小模型碰撞体积细节和碎片文件，减轻cpu负担
<div align="center">
  <img width="752" height="340" alt="image" src="https://github.com/user-attachments/assets/afa68618-b7db-407f-9798-cfa5c576684d" />
</div>


但是问题就出在这里!!!\
导入后不显示模型,由于完全不动只能求助AI\
先给出的建议是点击 so101_new_calib 按 F 键对焦——但是相机飞过去仍然看不见东西
claude进一步让我展开 Hierarchy 层级查看子对象——发现层级结构是有的

发现底部console报错说模型未加载好
<img width="2559" height="1520" alt="image" src="https://github.com/user-attachments/assets/c9bdb5c4-a394-4dd4-9f06-36a0fe769631" />
但并未发现未加载好的情况于是删掉空白object重新导入，

点进最深层的子对象看 Inspector——发现 Mesh Filter 里 mesh 和material是空的
这个结论的得出非常的折腾，最主要的问题是我完全不动导入Hierarchy里的文件结构和功能，可以从下面的一个分支的展开结构感受到这个开源模型文档的复杂程度
<img width="611" height="845" alt="image" src="https://github.com/user-attachments/assets/4651a3bf-af0f-4121-8aaa-b72fa7a3e386" />

而询问 AI 的过程就更加繁琐了。

由于 Claude 也不知道这个文件内部的具体结构是什么样的，它能看到的其实只有 Hierarchy 里面最外层的结构。比如它能看到某个对象前面有一个可以下拉的箭头，于是它知道下面应该还有一个层级，但它并不知道这个层级下面还有多少东西，也不知道真正需要找的组件到底藏在哪。

所以最开始，它让我去第一个层级截图，看有没有它需要的组件。我截给它，它说没有；然后让我再往下一层找，还是没有。就这样一层一层地往下。

但问题是，我其实完全不知道它在找什么。

它最开始只是说要找一个 Mesh 的东西，但我根本不知道这个东西是干什么用的，也不知道它会以什么形式存在。因为在我看来，里面大部分都是 Script、Transform 之类的组件，我根本不知道它是不是藏在某个脚本里面，或者是不是我已经看到了但自己没有意识到。

所以它所说的东西对我来说一直都是很模糊的。我能做的只有按照它的要求，一层一层地去筛选。截图、发送、等待回复；再截图、再发送、再等待回复。

一直筛到最后一层，它终于在右侧 Inspector 里看到了它想找的东西，但发现这个组件是空的。到这里，问题终于找到了。

但是整个搜索过程，以及应该如何提问、为什么要这样找，我始终都是模糊的。我并没有真正理解发生了什么，只是在机械地重复

<img width="2557" height="1529" alt="屏幕截图 2026-06-09 154009" src="https://github.com/user-attachments/assets/7301ce8f-df04-48dc-a4ef-be10425be418" />

<img width="2559" height="1518" alt="屏幕截图 2026-06-09 154528" src="https://github.com/user-attachments/assets/55e7a0f8-499b-419a-a5ae-4d71800f5ffc" />
<img width="2551" height="1519" alt="屏幕截图 2026-06-09 154523" src="https://github.com/user-attachments/assets/8b33691a-a9bc-42d6-98f6-1842ab292916" />
<img width="2553" height="1518" alt="屏幕截图 2026-06-09 154518" src="https://github.com/user-attachments/assets/b84ef80f-cd11-4afb-8e3c-cf499e0b888b" />
