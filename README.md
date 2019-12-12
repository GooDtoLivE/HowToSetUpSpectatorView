# HowToSetUpSpectatorView
搭建Hololens-SpectatorView环境
## Getting Started

### 获取官方源码

**当前，获取和使用Spectator View代码的受支持过程是通过将存储库作为子模块添加到您的项目中来进行** 从发布选项卡下载源代码，但是如果选择不引用代码库，则相关脚本和示例项目可能会中断。子模块。克隆和使用git存储库的步骤如下:

1. 下载 [git](https://git-scm.com/downloads)
2. 为您的项目设置存储库。有关如何设置存储库的更多信息，请参见 [这里](https://help.github.com/en/articles/create-a-repo).
3. 打开管理员命令窗口.
4. 克隆项目的存储库.
![Marker](SpectastorView/SpectastorView/CloneRepo.png)
5. 将目录更改为项目存储库的目录.
6. 通过运行 `git submodule add https://github.com/microsoft/MixedReality-SpectatorView.git sv`将MixedReality-SpectatorView代码库添加为项目的子模块
![Marker](SpectastorView/SpectastorView/AddSubmodule.png)

### 设置本地环境

**添加子模块**
1. 管理员身份运行Power shell，然后导航到项目文件夹中的SV文件夹
2. 运行 tools/Scripts/SetupRepository.bat命令
![Marker](SpectastorView/SpectastorView/SetupRepo.png)
3. 该命令会自动下载[MixedRealityToolkit-Unity](https://github.com/microsoft/MixedRealityToolkit-Unity)、[Azure-Spatial-Anchors-Samples](https://github.com/Azure/azure-spatial-anchors-samples) 、 [ARCore-Unity-SDK](https://github.com/google-ar/arcore-unity-sdk)
以上模块是当前项目中所包含的子模块

>Note: 如果下载过程中出现了中断或者未完成的情况，请直接在该处下载[MixedRealityToolkit-Unity](https://github.com/microsoft/MixedRealityToolkit-Unity/tree/b7dbeb6e9b14355ed176a388ddac3e4a4a1946f9)、[Azure-Spatial-Anchors-Samples](https://github.com/Azure/azure-spatial-anchors-samples/tree/61a1e390cb09ab7544da9304460f5b88e331a3ef) 、 [ARCore-Unity-SDK](https://github.com/google-ar/arcore-unity-sdk/tree/05829541bdf24c6dcbbeb5976dc1673c6a482471)将下载的文件解压后复制到工程下的sv\external\模块中的文件

**设置依赖关系**
1. 管理员身份运行Power shell，然后导航到项目文件夹中的SV文件夹
2. 运行tools\Scripts\AddDependencies.bat -AssetPath "Assets" -SVPath "sv"
图 ![Marker](SpectastorView/SpectastorView/AddDependencies.png)
>Note: 工程结构如下
>* **Project repository directory:** c:\Your\Unity\Project
>* **Project Assets directory:** c:\Your\Unity\Project\Assets
>* **MixedReality-SpectatorView submodule directory:** c:\Your\Unity\Project\sv

### Unity基础设置

1. 确保项目中包含了构建SpectatorView所需要的[软硬件](https://github.com/GooDtoLivE/MixedReality-SpectatorView/blob/master/doc/SpectatorView.Setup.md)

2. 完成 Getting Started以上步骤之后，项目会引用 MixedReality-SpectatorView codebase.

3. 添加 `MixedReality.SpectatorView/SpectatorView/Prefabs/SpectatorView.prefab` 到主场景. 这个 prefab 包含了大量的Spectator View code 用于跨设备之间的同步和对齐.

4. 选择 [Spatial Alignment Strategy](https://github.com/GooDtoLivE/MixedReality-SpectatorView/blob/master/src/SpectatorView.Unity/Assets/SpatialAlignment/README.md) 允许多个设备在物理世界中的同一位置查看holograms. 不同的机制实现对齐, 比如 [Azure Spatial Anchors](https://azure.microsoft.com/en-us/services/spatial-anchors/) 和 基于标记检测器的方法. 并非所有方法都适用于所有设备，因此需要选择最能满足您需求的策略.

5. 添加Unity项目的Spatial Alignment Strategy所需的 [依赖项](https://github.com/GooDtoLivE/MixedReality-SpectatorView/blob/master/doc/SpectatorView.Setup.md). 这涉及到更新 git submodules, 添加 symbolic linked 目录, 以及 手动下载和解压Zip文件. 完成此步骤后，将获得Unity项目中包含的外部项目中所有需要的代码.

6. 更新 Unity project 和 player settings 的 [需求](https://github.com/GooDtoLivE/MixedReality-SpectatorView/blob/master/doc/SpectatorView.Setup.md) Spatial Alignment Strategy. 通常涉及将预处理器指令添加到不同平台的player settings中，以启用特定于您所需的代码路径的 Spatial Alignment Strategy.

7. 生成并check-in Asset Caches到项目的 repository. 这些 Asset Caches 就像 GameObject registries 并允许不同的设备运行程序，去了解在整个软件运行周期中创建、销毁或更新了哪些Unity对象. 生成 asset caches, 运行 [Spectator View -> Update All Asset Caches](https://github.com/GooDtoLivE/MixedReality-SpectatorView/blob/master/doc/SpectatorView.Setup.md)在 Unity Editor toolbar.

8. 构建并部署主场景 HoloLens上.

9. 打开样例适用于移动设备的 spectating 场景. 应该是 `SpectatorView.Android.unity`, `SpectatorView.iOS.unity` 或者 `SpectatorView.HoloLens.Spectator.unity`.

    > Note: 创建自己的 spectating 场景, 确保 `SpectatorView` 对象的 `Role` 属性被设置为 `Spectator`;   在 `SpectatorView > SpatialCoordinateSystem > CameraTransform` 对象上的`Shared Coordinate Origin`属性被设置为主相机父节点对象.

10.构建并部署 spectating 场景到移动设备上. 确保在Build Setting是中包含了 `SpectatorView.Android.unity`, `SpectatorView.iOS.unity` 或者 `SpectatorView.HoloLens.Spectator.unity` 场景. 特定的平台构建说明可以在 [这里](https://github.com/GooDtoLivE/MixedReality-SpectatorView/blob/master/doc/SpectatorView.Setup.md)找到.

### 细节设置
有关设置SpectatorView项目更多的信息：
* [Spectating with an Android, an iOS or a HoloLens device](https://github.com/GooDtoLivE/MixedReality-SpectatorView/blob/master/doc/SpectatorView.Setup.md)
