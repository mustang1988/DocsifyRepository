# Windows下WebRTC源码编译

---

## 准备

1. 代理服务, 编译过程中有大量源码, 工具需要通过Git进行更新和下载, WebRTC相关的Git仓库均在Google域名下, 国内无法直接访问, 所以代理服务是必须的

2. 暂时删除本地已安装的Python的PATH环境变量配置, 编译中需要使用Google提供的编译工具包中指定版本的Python, 所以可能会与本地已经配置的版本发生冲突, 建议先删除本地已配置的Python环境变量, 尤其是PATH环境变量中的指向

3. 建议打开Windows设置中的"显示隐藏文件/文件夹选项"

4. Visual Studio 2015 及以上版本, 推荐使用 2019 或 2017 比较稳妥, 出错的概率会低很多

## 下载安装&更新 Deop Tools 工具包

下载安装 Deop Tools 有以下两种方式, 任选其一即可
- 通过Git下载

  ```bash
  git clone https://chromium.googlesource.com/chromium/Tools/depot_tools.git
  ```

- 下载压缩包

  [下载地址](https://storage.googleapis.com/chrome-infra/depot_tools.zip)

  下载后解压到独立目录下, 确保该目录所在磁盘分区的剩余可用空间 ***不低于20GB***, 本文中, 文件解压目录位于: D:\Code\WebRTC_Related\depot_tools

  !> 注意压缩包中包含一个隐藏目录".git", 需要一并解压出来, 建议打开Windows中的"显示隐藏文件/文件夹配置"方便查看

下载的压缩包解压完成或 git clone 完成后, 将解压目录配置到系统环境变量*PATH*中

打开终端或CMD, 执行以下命令以更新 Deop Tools 到最新, 此过程会使用git获取更新内容, 因此目录下的.git隐藏目录是必须的

```bash
gclient
```

## 获取 WebRTC 源码

创建独立目录用于存放WebRTC源码, 本文中该目录为: D:\Code\WebRTC_Related\webrtc-checkout

使用终端或CMD进入该目录, 拉取源码并更新相关子模块与依赖, 拉取地址位于google域名下, 国内无法直接访问, 请确保网络代理服务已完成配置并生效

```bash
cd D:\Code\WebRTC_Related\webrtc-checkout
fetch --nohooks webrtc
# 具体编译版本根据实际需要调整
git checkout branch-heads/m79
gclient sync
```

该步骤耗时会很久, 需要耐心等待, 期间会下载各种编译工具, 代码依赖, 源码等等

!> 下载的文件总量会超过10GB(2022年3月28日编译时, 实际下载量为15.7GB), 需要特别注意所在磁盘分区的剩余可用空间

## 生成 Ninja 构建目录

```bash
# 以下临时环境变量设置用于指定编译所用的VS版本, 仅针对同时安装了多个版本VS时需要设置
set GYP_MSVS_VERSON=2019
set vs2019_install=F:\vs2019
set GYP_MSVS_OVERRIDE_PATH=F:\vs2019
# 以上为安装了多版本VS时, 指定编译使用的VS所需要的临时环境变量
set DEPOT_TOOLS_WIN_TOOLCHAIN=0
cd src
gn gen out/Win64 --args="is_debug=false target_os=\"win\" target_cpu=\"x64\" is_component_build=false is_clang=false use_lld=false treat_warnings_as_errors=false use_rtti=true rtc_include_tests=false rtc_build_examples=false"
```

其中 *gn gen* 后的第一个参数为**构建目录**

*--args* 后的参数为编译参数

部分编译参数说明

|参数名|作用|默认值|
|:-|:-|:-|
|is_debug|执行debug编译|true|
|target_os|编译目标操作系统||
|target_cpu|编译的目标cpu指令集||
|is_component_build|是否作为单独组件构建|true|
|is_clang|是否支持c语言构建||
|rtc_include_tests|是否包含单元测试|true|
|rtc_build_examples|是否包含示例|true|
|rtc_use_h264|是否编译h264编解码支持|false|
|rtc_libvpx_build_vp9|是否编译vp9编解码支持||

## 执行编译

```bash
ninja -C [前一步指定的**构建目录**]
```

编译耗时大约5~10分钟

?> ninja 默认会启动多线程编译, 但多个线程的控制台输出是汇总到一起的, 当有其中某个线程编译报错或不通过, 只会在控制台末尾输出"build stopped: subcommand failed."错误, 此时该错误可能并不是当前控制台能看到的最后一个子编译任务抛出的, 需要往前找最近的error才能定位, 不是很方便排查, 可以添加 -l 1 参数, 只启用一个线程编译, 当报错发生时, 就可以快速定位产生报错的命令, 当然这也会大大降低编译速度, 增减编译的耗时

### 可能遇到的错误&解决方案

- 生成 Ninja 构建目录阶段, 报错: *缺少 dbghelp.dll*

  ![缺少 dbghelp.dll](../images/1.png)

  解决方案

  1. 点击 开始菜单 -> 设置 -> 应用, 在列表中找到对应版本的Windows SDK, 点击下方的"修改"按钮

    ![缺少 dbghelp.dll 错误](../images/2.png)

  2. 在弹出的安装向导中选择"修改", 点击"下一步"

  3. 勾选列表中的"Debugging Tools for Windows", 然后点击"更改"按钮

    ![缺少 dbghelp.dll 错误](../images/3.png)

## 参考文档

- [Windows平台WebRTC编译-VS2017](https://blog.jianchihu.net/webrtc-build-vs2017.html)
- [Google windows_build_instructions](https://chromium.googlesource.com/chromium/src/+/master/docs/windows_build_instructions.md#Visual-Studio)