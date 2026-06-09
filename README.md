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
<img width="2559" height="1520" alt="image" src="https://github.com/user-attachments/assets/c9bdb5c4-a394-4dd4-9f06-36a0fe769631" />


<img width="2557" height="1529" alt="屏幕截图 2026-06-09 154009" src="https://github.com/user-attachments/assets/7301ce8f-df04-48dc-a4ef-be10425be418" />

<img width="2559" height="1518" alt="屏幕截图 2026-06-09 154528" src="https://github.com/user-attachments/assets/55e7a0f8-499b-419a-a5ae-4d71800f5ffc" />
<img width="2551" height="1519" alt="屏幕截图 2026-06-09 154523" src="https://github.com/user-attachments/assets/8b33691a-a9bc-42d6-98f6-1842ab292916" />
<img width="2553" height="1518" alt="屏幕截图 2026-06-09 154518" src="https://github.com/user-attachments/assets/b84ef80f-cd11-4afb-8e3c-cf499e0b888b" />
