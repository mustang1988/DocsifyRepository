# ChildProcess模块

---

NodeJS的ChildProcess模块提供了"多进程"的支持, 使得我们可以通过新开进程来处理计算密集或IO密集型的长耗时任务, 这样可以充分利用CPU的计算资源

ChildProcess模块提供了以下API用来创建子进程
- exec(command[, options][, callback])
- execFile(file[, args][, options][, callback])
- fork(modulePath[, args][, options])
- spawn(command[, args][, options])
- execSync(command[, options])
- execFileSync(file[, args][, options])
- spawnSync(command[, args][, options])

---

## exec(command[, options][, callback])

开启一个Shell子进程, 然后在该Shell中执行命令, 传递给exec函数的命令字符串由shell直接处理

### 参数说明
- command, 需要执行的命令, 命令参数与命令之间用空格隔开
- options, 可选参数, *TODO内容待补充*
- callback, 可选参数, 执行结束后的回调函数, 回调函数参数列表如下:
  - error, 命令执行时发生的异常
  - stdout, 命令执行时的标准输出
  - stderr, 命令执行时的异常输出

### 返回值:

ChildProcess对象

### 使用示例

```javascript
// 使用 exec(command[, options][, callback]) 执行"ls -al /"命令
const { exec } = require('child_process');
const command = ['ls', '-al', '/'];
exec(command.join(' '), { encoding: 'utf8' }, (error, stdout, stderr) => {
  console.log({ error, stdout: stdout.toString(), stderr: stderr.toString() });
});
```

---

## execFile(file[, args][, options][, callback])

execFile()函数与exec()类似, 区别在于, 它在默认情况下不会生成Shell, 而是将指定的可执行文件直接作为一个新进程生成, 这使得它比exec()略高效, 支持与exec()相同的选项, 由于不生成Shell, 因此不支持I/O重定向和文件通配符等行为

### 参数说明
- file, 需要执行的文件
- args, 可选参数, 提交给file文件的执行参数
- options, 可选参数, *TODO内容待补充*
- callback, 可选参数, 执行结束后的回调函数, 回调函数参数列表如下:
  - error, 命令执行时发生的异常
  - stdout, 命令执行时的标准输出
  - stderr, 命令执行时的异常输出

### 返回值

ChildProcess对象

### 使用示例

```javascript
const {execFile} = require('child_process');
// *TODO内容待补充*
```

---

## fork(modulePath[, args][, options])

fork() 函数是spawn()函数的一个特例, 和 spawn() 函数一样, 生成新的Node.js进程并返回一个ChildProcess对象, 特殊之处在于返回的子进程将有一个额外的内置通信通道, 子进程允许通过该通信通道, 向父进程发送消息从而实现进程之间通信

### 参数说明
- modulePath, 子进程需要执行的js模块
- args, 可选参数, 子进程启动时接收的参数列表
- options, 可选参数, *TODO内容待补充*

### 返回值

ChildProcess对象

### 使用示例

```javascript
const {fork} = require('child_process');
// *TODO内容待补充*
```

---

## spawn(command[, args][, options])

使用指定的command命令和args参数, 创建子进程, 如果未指定args, 其值默认为空数组

!> 如果在spawn中通过可选参数启用了shell, 那么输入的参数需要注意进行检查, 否则可能存在被注入恶意shell脚本攻击

### 参数说明
- command, 需要执行的命令
- args, 可选参数, 提交给命令的参数
- options, 可选参数, *TODO内容待补充*

### 返回值

ChildProcess对象

### 使用示例

```javascript
const {spawn} = require('child_process');
// *TODO内容待补充*
```

---

## execSync(command[, options])

execSync() 函数是 [exec()](/repository/Languages/JavaScript/docs/ChildProcess.md#execcommand-options-callback) 函数的同步版本, 执行时会阻塞进程, 直到命令执行结束(不论进程是正常/非正常退出), 若执行时长超过可选参数中设定的超时时长, 则会中断执行.

### 参数说明
- command, 需要执行的命令
- options, 可选参数, *TODO内容待补充*

### 返回值

Buffer|string, 命令执行时的stdout

### 使用示例

```javascript
const {execSync} = require('child_process');
// *TODO内容待补充*
```

---

## execFileSync(file[, args][, options])

execFileSync() 函数是 [execFile()](/repository/Languages/JavaScript/docs/ChildProcess.md#execfilefile-args-options-callback) 函数的同步版本, 执行时会阻塞进程, 直到命令执行结束(不论进程是正常/非正常退出), 若执行时长超过可选参数中设定的超时时长, 则会中断执行.

### 参数说明
- file, 需要执行的文件
- args, 可选参数, 提交给file文件的执行参数
- options, 可选参数, *TODO内容待补充*

### 返回值

Buffer|string, 命令执行时的stdout

### 使用示例

```javascript
const {execFileSync} = require('child_process');
// *TODO内容待补充*
```

---

## spawnSync(command[, args][, options])

spawnSync() 函数是 [spawn()](/repository/Languages/JavaScript/docs/ChildProcess.md#spawncommand-args-options) 函数的同步版本, 执行时会阻塞进程, 直到命令执行结束(不论进程是正常/非正常退出), 若执行时长超过可选参数中设定的超时时长, 则会中断执行.

### 参数说明
- command, 需要执行的命令
- args, 可选参数, 提交给命令的参数
- options, 可选参数, *TODO内容待补充*

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
// *TODO内容待补充*
```
