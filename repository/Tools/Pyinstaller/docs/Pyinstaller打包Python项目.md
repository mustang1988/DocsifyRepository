# Pyinstaller打包Python项目

---

## 为何需要对 Python 项目进行打包?

通常情况下 Python 项目都是直接部署源码运行的

但是当发生客户定制功能, 私有化部署的时候, 为了保护源码, 避免客户随意更改, 隐藏源码只提供可执行版本就很有必要

通常情况下在发生私有化部署, 为保护源码, 一般可以选择将源码 .py 统一编译为 .pyc 字节码再部署给客户, 但是 .pyc 字节码文件, 是存在被反编译的风险的, 反编译后, 客户依然可以修改源码, 达到一些不可告人的目的; 于此同时当项目复杂度很高, 外部依赖组件/模块/服务/静态资源文件等等较多, 复杂度较高, 仅编译 Python 脚本后部署就变得不可行了, 此时打包编译项目为对应平台的可执行文件, 直接给客户提供编译后的可执行文件就很有必要了

对于图形化界面的 Python 客户端/插件, 也需要只向用户提供打包后的可执行文件或安装包, 源码是不提供的, 除非项目是有开源许可证的.

Pyinstaller 就是为了这些种特定需求而存在的打包工具

## 如何使用 Pyinstaller 打包 Python 项目

### Pyinstaller 安装

```bash
pip install pyinstaller
```

### Pyinstaller 参数详解

- --distpath DIR

    打包后的输出路径, 可选参数, 默认值: ./dist

- --workpath WORKPATH

    打包编译的临时路径, 可选参数, 默认值: ./build

- --clean

    执行构建前清空缓存和临时目录

- --log-level LEVEL

    构建时控制台输出日志级别, 可选参数, 默认值: INFO

- -D 或 --onedir

    构建并输出包含可执行文件的目录

- -F 或 --onefile

    构建并输出单一可执行文件

- --specpath DIR

    存储构建生成的spec文件的目录

- -n NAME 或 --name NAME

    输出可执行文件的名称, 可选参数, 默认值: 同入口py脚本文件名

- --add-data <SRC;DEST or SRC:DEST>

    添加静态资源文件或文件夹

- -add-binary <SRC;DEST or SRC:DEST>

    添加可执行文件或文件夹

- -p DIR 或 --paths DIR

    代码引用文件检索目录

- -hidden-import MODULENAME 或 --hiddenimport MODULENAME

    代码中非直接引用的模块或脚本名称

### spec 配置文件详解

在首次使用pyinstaller命令执行文件打包后, 默认会在当前目录下生成.spec配置文件

该配置文件的主要作用是持久化存储打包的参数, 后续执行打包时不用再输入冗长的打包参数, 而是指定使用编写好的 .spec 文件即可

.spec 文件基本格式如下

```python
# -*- mode: python -*-

block_cipher = None


a = Analysis(['入口py脚本'],
             pathex=['入口py脚本所在目录'],
             binaries=[],
             datas=[],
             hiddenimports=[],
             hookspath=[],
             runtime_hooks=[],
             excludes=[],
             win_no_prefer_redirects=False,
             win_private_assemblies=False,
             cipher=block_cipher,
             noarchive=False)
pyz = PYZ(a.pure, a.zipped_data,
             cipher=block_cipher)
exe = EXE(pyz,
          a.scripts,
          a.binaries,
          a.zipfiles,
          a.datas,
          [],
          name='应用名称, 默认同入口py脚本的文件名',
          debug=False,
          bootloader_ignore_signals=False,
          strip=False,
          upx=True,
          runtime_tmpdir=None,
          console=True )
```

该配置文件中, 支持上述罗列的 pyinstaller 参数

其中
- Analysis 下的 pathex 作用等同于命令参数 [-p DIR 或 --paths DIR](https://www.notion.so/p-DIR-paths-DIR-c143841ab0b9459994e26b3937fbfa10)
- Analysis 下的 datas 作用等同于命令参数 [--add-data <SRC;DEST or SRC:DEST>](https://www.notion.so/add-data-SRC-DEST-or-SRC-DEST-8479e6115ae94731b1d69e48622f7a17)
- Analysis 下的 binaries 作用等同于命令参数 [-add-binary <SRC;DEST or SRC:DEST>](https://www.notion.so/add-binary-SRC-DEST-or-SRC-DEST-4e7ecd1a309041ad826934a234cb5ff5)
- Analysis 下的 hiddenimports 作用等同于命令参数 [-hidden-import MODULENAME
或
 --hiddenimport MODULENAME](https://www.notion.so/hidden-import-MODULENAME-hiddenimport-MODULENAME-23223a66c2d7424093cec5372a74ea6a)
- EXE 下的 name 作用等同于命令参数 [-n NAME 或 --name NAME](https://www.notion.so/n-NAME-name-NAME-61e27461fc054d7888632040dcb721d7)

### 静态资源文件的打包

以使用 .spec 文件打包为例, 将当前目录下的 a.txt 文件和 assert目录添加到最终打包的可执行文件, 配置如下

```python
a = Analysis(['入口py脚本'],
             pathex=['入口py脚本所在目录'],
             binaries=[],
             datas=[('a.txt','a.txt'),('assert','assert')],
             hiddenimports=[],
             hookspath=[],
             runtime_hooks=[],
             excludes=[],
             win_no_prefer_redirects=False,
             win_private_assemblies=False,
             cipher=block_cipher,
             noarchive=False)
```

### 执行打包

```bash
# 直接打包
pyinstaller -F 入口python脚本.py
# 使用spec配置文件打包
pyinstaller -F xxx.spec
```
