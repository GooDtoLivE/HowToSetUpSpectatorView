# HowToSetUpSpectatorView
搭建Hololens-SpectatorView环境
## Getting Started

### Obtaining the code

**当前，获取和使用Spectator View代码的受支持过程是通过将存储库作为子模块添加到您的项目中来进行** 从发布选项卡下载源代码，但是如果选择不引用代码库，则相关脚本和示例项目可能会中断。子模块。克隆和使用git存储库的步骤如下:

1. 下载 [git](https://git-scm.com/downloads)
2. 为您的项目设置存储库。有关如何设置存储库的更多信息，请参见 [here](https://help.github.com/en/articles/create-a-repo).
3. 打开管理员命令窗口.
4. 克隆项目的存储库.
5. 将目录更改为项目存储库的目录.
6. 通过运行 `git submodule add https://github.com/microsoft/MixedReality-SpectatorView.git sv`将MixedReality-SpectatorView代码库添加为项目的子模块
图

### Setting up your local environment

**Add SubModules**
1. 管理员身份运行Power shell，然后导航到项目文件夹中的SV文件夹
2. 运行 tools/Scripts/SetupRepository.bat命令
图
3. 该命令会自动下载[MixedRealityToolkit-Unity](https://github.com/microsoft/MixedRealityToolkit-Unity)、[Azure-Spatial-Anchors-Samples](https://github.com/Azure/azure-spatial-anchors-samples) 、 [ARCore-Unity-SDK](https://github.com/google-ar/arcore-unity-sdk)
以上模块是当前项目中所包含的子模块

>Note: 如果下载过程中出现了中断或者未完成的情况，请直接在该处下载[MixedRealityToolkit-Unity](https://github.com/microsoft/MixedRealityToolkit-Unity/tree/b7dbeb6e9b14355ed176a388ddac3e4a4a1946f9)、[Azure-Spatial-Anchors-Samples](https://github.com/Azure/azure-spatial-anchors-samples/tree/61a1e390cb09ab7544da9304460f5b88e331a3ef) 、 [ARCore-Unity-SDK](https://github.com/google-ar/arcore-unity-sdk/tree/05829541bdf24c6dcbbeb5976dc1673c6a482471)将下载的文件解压后复制到工程下的sv\external\模块中的文件

**设置依赖关系**
1.管理员身份运行Power shell，然后导航到项目文件夹中的SV文件夹
2.运行tools\Scripts\AddDependencies.bat -AssetPath "Assets" -SVPath "sv"

>Note: 工程结构如下

Project repository directory: c:\Your\Unity\Project
Project Assets directory: c:\Your\Unity\Project\Assets
MixedReality-SpectatorView submodule directory: c:\Your\Unity\Project\sv
