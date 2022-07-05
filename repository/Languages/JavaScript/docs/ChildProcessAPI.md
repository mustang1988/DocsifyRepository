# ChildProcess对象API

---

ChildProcess对象中包含以下可访问属性

- [channel](#channel)
- [connected](#connected)
- [exitCode](#exitCode)
- [killed](#killed)
- [pid](#pid)
- [signalCode](#signalCode)
- [spawnargs](#spawnargs)
- [spawnfile](#spawnfile)
- [stderr](#stderr)
- [stdin](#stdin)
- [stdout](#stdout)
- [stdio](#stdio)

和以下可调用方法

- [channel.ref()](#channelref)
- [channel.unref()](#channelunref)
- [kill()](#killsignal)
- [disconnect()](#disconnect)
- [ref()](#ref)
- [send()](#sendmessage-sendhandle-options-callback)
- [unref()](#unref)


## 属性

### channel

该属性为子进程的IPC通道的引用, 如果没有IPC通道, 该属性值为undefined

#### 示例

```javascript
const { fork, exec } = require('child_process');
const child_exec = exec('ls -al /');
console.log(child_exec.channel);// undefined
// ============================================
const child_fork = fork('./sub_module.js');
console.log(child_fork.channel);
/**
Control {
    _events: [Object: null prototype] {},
    _eventsCount: 0,
    _maxListeners: undefined,
    [Symbol(kCapture)]: false,
    [Symbol(kPendingMessages)]: []
}
 */

```

### connected

该属性标识子进程是否仍然可以和主线程进行通信, 如果值为false, 则子进程无法接收主线程发送的消息, 也无法向主线程发送消息

#### 示例

```javascript
const { fork } = require('child_process');
const child_fork = fork('dir', ['C:\\']);
console.log(child_fork.connected); // true
child_fork.disconnect();
console.log(child_fork.connected); // false
```

### exitCode

该属性标识子进程的退出状态码, 如果子进程尚未退出, 该属性值为null

#### 示例

```javascript
const { exec } = require('child_process');
const child_exec = exec('dir C:\\');
child_exec.on('close', (code, signal) => {
  console.log(child_exec.exitCode); // 0
});
```

### killed

该属性标致子进程是否被中断, true为中断, false为未中断

#### 示例

```javascript
const { exec } = require('child_process');
const child_exec = exec('dir C:\\');
console.log(child_exec.killed); // false
```

### pid

该属性为子进程的PID, 如果子进程派生失败或发生异常, 该属性值为undefined, 同时会触发 [error](/repository/Languages/JavaScript/docs/ChildProcessEvents.md#error) 事件

#### 示例

```javascript
const { exec } = require('child_process');
const child_exec = exec('dir C:\\');
console.log(child_exec.pid);
```

### signalCode

该属性为子进程的退出状态码, 如果子进程尚未退出, 该属性值为null

#### 示例

```javascript
const { exec } = require('child_process');
const child_exec = exec('dir C:\\');
child_exec.kill('SIGTERM');
child_exec.on('close', (code, signal) => {
  console.log(child_exec.signalCode); // 'SIGTERM'
});
```

### spawnargs

该属性为子进程执行命令的完整参数列表

#### 示例

```javascript
const { exec } = require('child_process');
const child_exec = exec('dir C:\\');
console.log(child_exec.spawnargs); // [ 'C:\Windows\system32\cmd.exe', '/d', '/s', '/c', '"dir C:\"' ]
```

### spawnfile

该属性为子进程执行的可执行文件名称

- [fork()](/repository/Languages/JavaScript/docs/ChildProcess.md#forkmodulepath-args-options) 创建的子进程, 该属性值为: process.execPath
- [spawn()](/repository/Languages/JavaScript/docs/ChildProcess.md#spawncommand-args-options) 创建的子进程, 该属性值为: 可执行文件的名称
- [exec()](/repository/Languages/JavaScript/docs/ChildProcess.md#execcommand-options-callback) 创建的子进程, 该属性值为: 子进程启动的Shell的名称

#### 示例

```javascript
const { exec } = require('child_process');
const child_exec = exec('dir C:\\');
console.log(child_exec.spawnfile); // 'C:\Windows\system32\cmd.exe'
```

### stderr

该属性为包含子进程运行时stderr信息的可读的流对象

#### 示例

```javascript
const { exec } = require('child_process');
const child_exec = exec('dir C:\\');
console.log(child_exec.stderr); // Socket {...}
```

### stdin

该属性为包含子进程运行时stdin信息的可读的流对象

#### 示例

```javascript
const { exec } = require('child_process');
const child_exec = exec('dir C:\\');
console.log(child_exec.stdin); // Socket {...}
```

### stdio

该属性为包含了stdin, stdout, stderr信息的数组, 默认情况下:

- stdio[0], 为 stdin
- stdio[1], 为 stdout
- stdio[2], 为 stderr

#### 示例

```javascript
const { exec } = require('child_process');
const child_exec = exec('dir C:\\');
console.log(child_exec.stdio); // [Socket {...},Socket {...},Socket {...}]
```

### stdout

该属性为包含子进程运行时stdout信息的可读的流对象

#### 示例

```javascript
const { exec } = require('child_process');
const child_exec = exec('dir C:\\');
console.log(child_exec.stdout); // Socket {...}
```

## 方法

### channel.ref()

如果之前调用过 [unref()](#unref) 方法, 则此方法使IPC通道保持父进程的事件循环运行

#### 示例

```javascript
const { fork } = require('child_process');
const child_fork = fork('dir', ['C:\\']);
child_fork.channel.ref();
```

### channel.unref()

此方法使IPC通道不保持父进程的事件循环运行，并允许它在通道打开时完成

#### 示例

```javascript
const { fork } = require('child_process');
const child_fork = fork('dir', ['C:\\']);
child_fork.channel.unref();
```

### kill([signal])

#### 参数

- signal: Node.Signal|String, 子进程退出信号

此方法用于向子进程发送中断信号, 如果有指定可选参数signal, 则子线程会在 [close](/repository/Languages/JavaScript/docs/ChildProcessEvents.md#close) 事件的回调函数中得到该信号, 如果未指定signal参数, 则会在 [close](/repository/Languages/JavaScript/docs/ChildProcessEvents.md#close) 事件回调函数中返回, 子进程创建时指定的可选参数option中指定的信号或其默认值: SIGTERM

#### 返回值

子进程中断成功时返回true, 中断失败时返回false

#### 示例

```javascript
const { fork } = require('child_process');
const child_fork = fork('dir', ['C:\\']);
console.log(child_fork.kill('SIGTERM')); // true
```

### disconnect()

此方法用于关闭主进程和子进程之间的IPC通道, 允许子进程在没有其他连接保持活动状态时优雅地退出, 调用后主进程和子进程的 [connected](#connected) 属性值均会被设置为false

#### 示例

```javascript
const { fork } = require('child_process');
const child_fork = fork('dir', ['C:\\']);
console.log(child_fork.connected); // true
child_fork.disconnect();
console.log(child_fork.connected); // false
```

### ref()

在调用 [unref()](#unref) 函数后调用此方法, 可以为子进程恢复被删除的在主进程事件循环中的引用计数, 以强制主进程在子进程退出后才可以退出

#### 示例

```javascript
const { fork } = require('child_process');
const child_fork = fork('dir', ['C:\\']);
child_fork.ref();
```

### send(message[, sendHandle[, options]][, callback])

此方法用于在主进程和子进程的IPC通道间进行进程间通信, 如果主进程和子进程间没有IPC通道([channel](#channel) 属性值为 undefined)时, 无法调用

#### 参数

- message: Object|String, 进程间通信消息
- sendHandle: Socket, 可选参数, net.Socket 对象或 net.Server 对象或undefined
- options: Object, 可选参数, 可选属性如下:
    - keepOpen: Boolean, handle 为 net.Socket 时生效, 值为true时, socket连接会保持open, 默认值: false
- callback: Function, 可选参数, 发送消息后的回调函数

#### 返回值

消息发送成功时返回true, 失败时返回false

#### 示例

```javascript
const { fork } = require('child_process');
const child_fork = fork('dir', ['C:\\']);
console.log(child_fork.send({ str: 'hello world' })); // true
```

### unref()

默认情况下, 主进程总是等待子进程退出后才可以退出, 此防范可以从主进程的事件循环中移除子进程的引用计数, 以允许主进程可以独立于子进程之外单独进行退出, 除非主进程和子进程之前存在IPC通道

#### 示例

```javascript
const { fork } = require('child_process');
const child_fork = fork('dir', ['C:\\']);
child_fork.unref();
```