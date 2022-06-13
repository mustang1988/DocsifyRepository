# Windows下编译支持NVENC编码器的FFmpeg

---

!> 该文档内容待补充 **TODO**

## 环境准备

Windows下需要MSYS2作为编译环境

### MSYS2的安装

1. 下载MSYS2的安装程序

  下载页面: [https://www.msys2.org/](https://www.msys2.org/)

  下载后运行, 默认安装路径位于: *c:/msys64*

  ?> 安装完成后, 可选择将安装路径加入到PATH环境变量中, 非必须

2. 更新基础依赖

  打开 *msys2.exe*, 在终端中执行命令

  ```bash
  pacman -Syu
  ```

3. 安装通用依赖

  执行以下命令

  ```
  pacman -S make diffutils yasm nasm
  ```

4. 执行完成后关闭MSYS2的bash窗口

#### 可能出现的问题与解决方案

- 下载更新和依赖时发生超时或下载更新过慢
  
  设置pacman的仓库地址为清华大学开源镜像站, 步骤如下:

  1. 使用文本编辑器打开MSYS2安装目录下的 */etc/pacman.d/**mirrors.mingw32*** 在首行添加以下内容
  ```
  Server = https://mirrors.tuna.tsinghua.edu.cn/msys2/mingw/i686
  ```
  2. 使用文本编辑器打开MSYS2安装目录下的 */etc/pacman.d/**mirrorlist.mingw64*** 在首行添加以下内容
  ```
  Server = https://mirrors.tuna.tsinghua.edu.cn/msys2/mingw/x86_64
  ```
  3. 使用文本编辑器打开msys2安装目录下的 */etc/pacman.d/**mirrorlist.msys*** 在首行添加以下内容
  ```
  Server = https://mirrors.tuna.tsinghua.edu.cn/msys2/msys/$arch
  ```
  4. 修改完成后, 重试更新/安装依赖的命令

- 安装依赖时出现 "signature from xxx" 异常
  
  更新数字签名包, 操作步骤如下:

  1. 执行以下命令
  ```
  pacman -S msys2-keyring
  ```
  2. 执行结束后, 重试更新/安装依赖的命令

## 源码准备

- *ffmpeg*

  使用 git clone 或访问 [ffmpeg官方站点](https://ffmpeg.org) 下载源码压缩包, 将源码文件置于MSYS2安装目录下的 *home/<用户名>/ffmpeg* 目录中

- *libx264*

  使用 git clone 或访问 [libx264](https://www.videolan.org/developers/x264.html) 下载源码压缩包, 将源码文件置于MSYS2安装目录下的 *home/<用户名>/x264* 目录中

- *nv-codec-headers*

  MSYS2安装目录下的 *home/<用户名>* 目录中使用 git clone 拉取[git clone https://git.videolan.org/git/ffmpeg/nv-codec-headers.git](git clone https://git.videolan.org/git/ffmpeg/nv-codec-headers.git)

## 编译安装

- *编译安装 nv-codec-headers*

  打开msys2.exe, 执行以下命令

  ```bash
  cd nv-codec-headers
  make && make install
  ```

- *编译 FFmpeg*
