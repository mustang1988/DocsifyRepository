# Unreal Engine 源码使用

---

## 源码获取

[Unreal Engine 官方仓库](https://github.com/EpicGames/UnrealEngine)

> 注意，该仓库并非Public的，需要先加入 EpicGames 的组织后才可以访问该仓库

使用 Git Clone 仓库源码到本地或下载Release列表中对应版本的ZIP包

## 环境准备

具体环境准备可参考 [UE 官方说明文档](https://docs.unrealengine.com/4.27/en-US/Basics/InstallingUnrealEngine/RecommendedSpecifications/) 的要求

## 依赖处理

执行源码目录中的 Setup.bat 脚本文件，其会自动检查和处理所需的依赖组件，此步骤会比较耗时需要耐心等待

## 生成VS解决方案

执行源码目录中的 GenerateProjectFiles.bat 脚本文件，会在目录下生成 VS 用解决方案文件

## 编译&调试

使用 VS 打开上一步生成的解决方案文件，将运行模式调整为开发模式，即可开始编译与调试，初次编译大约需要消耗10~40分钟的时间，具体时长视开发机配置而定