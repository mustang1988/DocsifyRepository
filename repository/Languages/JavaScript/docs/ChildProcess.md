# ChildProcess模块

---

NodeJS的ChildProcess模块提供了"多进程"的支持, 使得我们可以通过新开进程来处理计算密集或IO密集型的长耗时任务, 这样可以充分利用CPU的计算资源

ChildProcess模块提供了以下API用来创建子进程
- [exec(command[, options][, callback])](#execcommand-options-callback)
- [execFile(file[, args][, options][, callback])](#execfilefile-args-options-callback)
- [fork(modulePath[, args][, options])](#forkmodulepath-args-options)
- [spawn(command[, args][, options])](#spawncommand-args-options)
- [execSync(command[, options])](#execsynccommand-options)
- [execFileSync(file[, args][, options])](#execfilesyncfile-args-options)
- [spawnSync(command[, args][, options])](#spawnsynccommand-args-options)

---

## exec(command[, options][, callback])

开启一个Shell子进程, 然后在该Shell中执行命令, 传递给exec函数的命令字符串由Shell直接处理

### 参数说明
- command, 需要执行的命令, 命令参数与命令之间用空格隔开
- options, 可选参数, 参考:[可选参数option](#关于可选参数option)
- callback, 可选参数, 执行结束后的回调函数, 回调函数参数列表如下:
  - error, 命令执行时发生的异常
  - stdout, 命令执行时的标准输出
  - stderr, 命令执行时的异常输出

### 返回值:

ChildProcess对象

### 使用示例

```javascript
const { exec } = require('child_process');
const command = ['ls', '-al', '/'].join(' ');
exec(command, (error, stdout, stderr) => {
  console.log('Child Process exec(): ', { error, stdout: stdout.toString(), stderr: stderr.toString() });
});
```

---

## execFile(file[, args][, options][, callback])

execFile()函数与 [exec()](#execcommand-options-callback) 类似, 区别在于

execFile() 默认情况下**不会**生成Shell, 而是将指定的可执行文件直接作为一个新进程生成, 这使得它比 [exec()](#execcommand-options-callback) 略高效

execFile() 由于不生成Shell, 因此不支持I/O重定向和文件通配符等行为

### 参数说明
- file, 需要执行的文件
- args, 可选参数, 提交给file文件的执行参数
- options, 可选参数, 参考:[可选参数option](#关于可选参数option)
- callback, 可选参数, 执行结束后的回调函数, 回调函数参数列表如下:
  - error, 命令执行时发生的异常
  - stdout, 命令执行时的标准输出
  - stderr, 命令执行时的异常输出

### 返回值

ChildProcess对象

### 使用示例

```javascript
const {execFile} = require('child_process');
const file = 'ffprobe';
const args = ['-v', '0', '-of', 'json', '-show_streams', '-i', 'test.mp4'];
execFile(file, args, (error, stdout, stderr) => {
  console.log('Child Process execFile(): ', {error, stdout, stderr});
});
```

---

## fork(modulePath[, args][, options])

fork() 函数是 [spawn()](#spawncommand-args-options) 函数的一个特例

和 [spawn()](spawncommand-args-options) 函数一样, 生成新的Node.js进程并返回一个ChildProcess对象

特殊之处在于返回的子进程将有一个额外的内置通信通道, 子进程允许通过该通信通道, 向父进程发送消息从而实现进程之间通信

### 参数说明
- modulePath, 子进程需要执行的js模块
- args, 可选参数, 子进程启动时接收的参数列表
- options, 可选参数, 参考:[可选参数option](#关于可选参数option)

### 返回值

ChildProcess对象

### 使用示例

```javascript
// main.js 主进程脚本
const {fork} = require('child_process');
const sub_module = require('./sub_process');
const sub_process = fork(sub_module);
// 主进程通过IPC通道发送消息给子进程
sub_process.send({data:'data to sub module'});
// 主进程接收子进程通过IPC通道发送的消息
sub_process.on('message', (msg_from_sub_module) => {
  console.log('Message From sub module: ', msg_from_sub_module);// {data:'data to parent'}
})

// sub_process.js 子进程脚本
// 子进程接收主进程通过IPC通道发送的消息
process.on('message', (msg_from_parent_process) => {
  console.log('Message From parent process: ', msg_from_parent_process);// {data:'data to sub module'}
  // 子进程通过IPC通道发送消息给主进程
  process.send && process.send({data:'data to parent'});
});
```

---

## spawn(command[, args][, options])

使用指定的command命令和args参数, 创建子进程, 如果未指定args, 其值默认为空数组

### 参数说明
- command, 需要执行的命令
- args, 可选参数, 提交给命令的参数
- options, 可选参数, 参考:[可选参数option](#关于可选参数option)

### 返回值

ChildProcess对象

### 使用示例

```javascript
const {spawn} = require('child_process');
const command = 'ffprobe';
const args = ['-v', '0', '-of', 'json', '-show_streams', '-i', 'test.mp4']
const child_p = spawn(command, args);
child_p.on('close', (code, signal) => {
  console.log('Spawn on close: ', { code, signal });
});
```

---

## execSync(command[, options])

execSync() 函数是 [exec()](execcommand-options-callback) 函数的同步版本, 执行时会阻塞进程, 直到命令执行结束(不论进程是正常/非正常退出), 若执行时长超过可选参数中设定的超时时长, 则会中断执行

### 参数说明
- command, 需要执行的命令
- options, 可选参数, 参考:[可选参数option](#关于可选参数option)

### 返回值

Buffer|string, 命令执行时的stdout

### 使用示例

```javascript
const {execSync} = require('child_process');
const command = ['ffprobe','-v', '0', '-of', 'json', '-show_streams', '-i', 'test.mp4'].join(' ');
const buffer = execSync(command);
console.log(buffer.toString());
```

---

## execFileSync(file[, args][, options])

execFileSync() 函数是 [execFile()](#execfilefile-args-options-callback) 函数的同步版本, 执行时会阻塞进程, 直到命令执行结束(不论进程是正常/非正常退出), 若执行时长超过可选参数中设定的超时时长, 则会中断执行.

### 参数说明
- file, 需要执行的文件
- args, 可选参数, 提交给file文件的执行参数
- options, 可选参数, 参考:[可选参数option](#关于可选参数option)

### 返回值

Buffer|string, 命令执行时的stdout

### 使用示例

```javascript
const {execFileSync} = require('child_process');
const file = 'ffprobe';
const args = ['-v', '0', '-of', 'json', '-show_streams', '-i', 'test.mp4'];
const buffer = execFileSync(file, args);
console.log(buffer.toString());
```

---

## spawnSync(command[, args][, options])

spawnSync() 函数是 [spawn()](#spawncommand-args-options) 函数的同步版本, 执行时会阻塞进程, 直到命令执行结束(不论进程是正常/非正常退出), 若执行时长超过可选参数中设定的超时时长, 则会中断执行.

### 参数说明
- command, 需要执行的命令
- args, 可选参数, 提交给命令的参数
- options, 可选参数, 参考:[可选参数option](#关于可选参数option)

### 返回值

Object, 包含以下属性:

- pid, 子进程的PID
- output, <Array>, stdio输出结果
- stdout, <Buffer|string>, 命令执行时的stdout(output[1])
- stderr, <Buffer|string>, 命令执行时的stderr(output[2])
- status, <number|null>, 命令执行的返回码, 如果命令异常中断, 该字段值为null
- signal, <string|null>, 命令终端信号, 如果命令正常结束, 该字段值为null
- error, 命令执行失败或超时导致的异常对象

### 使用示例

```javascript
const {spawnSync} = require('child_process');
const file = 'ffprobe';
const args = ['-v', '0', '-of', 'json', '-show_streams', '-i', 'test.mp4'];
const result = spawnSync(file, args);
const {pid, output, stdout, stderr, status, signal, error} = result;
console.log(result);
```

## 关于可选参数option

ChildProcess模块提供API函数中均有一个可选参数option, 其作用是定义一些可选命令选项, 可选项如下:

!> 注意: 以下可选参数**并不是**ChildProcess提供的**所有**API函数均支持, 部分参数仅在某几个API函数中可用

- cwd, 子进程工作目录, 默认值: 主进程的 process.cwd()

- env, 子进程的环境变量配置, 默认值: 主进程的 process.env

- encoding, 子进程命令的字符集, 默认值: utf8

- shell
  
  - 设置执行命令的Shell, 在Unix系统下默认值: /bin/sh, Windows系统下默认值: process.env.ComSpec
  
  - 在部分ChildProcess的API函数中, 该参数为boolean值, 用于设置是否创建Shell来执行命令, 默认值: false
  
  !> 注意: 如果设置为true, 则对于输入的参数需要进行检查, 否则可能存在被注入恶意shell脚本攻击的风险

- signal, 允许使用的命令中断信号值

- timout, 命令执行的超时时长, 默认值: 0

- maxBuffer, 命令执行时stderr和stdout允许的最大字节数, 默认值: 1024*1024

- killSignal, 子进程kill信号, 默认值: SIGTERM

- uid, 子进程执行的用户唯一标识

- gid, 子进程执行的用户组唯一标识

- windowsHide, 隐藏子进程执行的命令窗口, 通常在Windows系统下会在子进程执行时被操作系统创建, 默认值: false

- windowsVerbatimArguments, 在Windows上不需要引用或转义参数, 在Unix系统下忽略此设置, 默认值: false

  在 [spawn()](#spawncommand-args), [spawnSync()](#spawnsynccommand-args), [execFile()](#execfilefile-args-callback), [fork()](#forkmodulepath-args) 函数中支持此参数

- detached, 允许子进程独立于主进程运行, 默认值: false

  在Windows上, 将options.detached设置为true可以使子进程在父进程退出后继续运行, 子进程将拥有自己的控制台窗口, 一旦为子进程启用, 它就不能被禁用
  
  在非windows平台上, 如果options.detached被设置为true, 子进程将成为一个新进程组和会话的领导者, 子进程可以在父进程退出后继续运行, 无论它们是否分离

  默认情况下, 父进程将等待分离的子进程退出, 要防止父进程等待给定的子进程退出, 请使用subprocess.unref()方法, 这样做将导致父进程的事件循环的引用计数中不包含子进程, 允许父进程独立于子进程退出, 除非子进程和父进程之间建立了IPC通道
  
  当使用detached选项启动一个长时间运行的进程时, 进程将不会在父进程退出后继续在后台运行, 除非它提供了一个没有连接到父进程的stdio配置, 如果继承了父级的stdio, 子级将继续连接到控制终端

- stdio, 用于设置子进程于主进程见通信的管道, 默认情况下, 子进程的stdin, stdout和stderr被重定向到相应的子进程ChildProcess对象的 subprocess.stdin, subprocess.stdout和subprocess.stderr中, 此时stdio属性的配置值相当于['pipe', 'pipe', 'pipe']即默认值

  其他可选值:

  - overlapped
  - ipc
  - ignore
  - inherit
  - Stream对象

- serialization, 用于设置进程间通信消息的序列化方式, 默认值: json, 可选值: json, advanced

  设置为advanced时, 会使用v8引擎的序列化API对消息进行序列化, 该序列化模块支持更多的JavaScript内置类型的序列化, 比如 RegExp 对象, 但因为该格式并不是JSON的超集, 所以会存在序列化后不兼容属性的丢失或格式变化, 从而导致在接收端接收消息并反序列化后无法读取指定属性的问题.

## 关于子进程ChildProcess

- [ChildProcess事件](/repository/Languages/JavaScript/docs/ChildProcessEvents.md#childprocess事件)
- [ChildProcess对象API](/repository/Languages/JavaScript/docs/ChildProcessAPI.md#childprocess对象api)