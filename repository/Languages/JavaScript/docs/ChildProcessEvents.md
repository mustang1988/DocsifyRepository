# ChildProcess事件

---

## close

### 事件触发条件

当进程结束**且**子进程的stdio流被关闭后触发

### 回调函数

close事件回调函数中包含以下2个参数:

- code: Number|null, 子进程的退出状态码
- signal: Node.Signal|null, 子进程终端信号

!> 注意: 需要区别 close 事件和[exit](#exit)事件, 当 [exit](#exit) 事件触发时, stdio流可能并未关闭, 此时并不会触发close事件, 只有stdio流关闭后才会触发close事件, 即 [exit](#exit) 和 close 事件的触发可能并不是同时的, 但 close 事件的触发总是会在 [exit](#exit) 事件触发之后

?> 如果有需求需要在子进程运行结束后执行一些处理逻辑, 最好将这部分相关逻辑放到close事件的回调函数中, 不建议放到 [exit](#exit) 的事件回调中.

### 示例

```javascript
const { exec } = require('child_process');
const command = 'ls -al /';
const child_p = exec(command);
child_p.on('close', (code, signal) => {
    console.log('Child Process on close: ', { code, signal });
});
```

## disconnect

### 事件触发条件

当在主进程中调用子进程对象的disconnect()函数或在子进程中调用主进程对象的disconnect()函数时触发

当触发该事件后, 子进程和主进程将不再允许使用 [send()](/repository/Languages/JavaScript/docs/ChildProcessAPI.md#subprocesssendmessage-sendhandle-options-callback) 函数进行进程间通信, 此时子进程的 [connected](/repository/Languages/JavaScript/docs/ChildProcessAPI.md#subprocessconnected) 属性将被设置为false

### 回调函数

disconnect事件回调函数无参数

### 示例

```javascript
const { exec } = require('child_process');
const command = 'ls -al /';
const child_p = exec(command);
child_p.on('disconnect', () => {
    console.log('Child Process on disconnect');
});
```

## error

### 事件触发条件

发生以下情况之一时, 触发该事件

1. 无法派生进程
2. 无法终中断进程
3. 向子进程发送消息失败

### 回调函数

error事件回调函数包含1个参数

- error: Error, 异常错误对象

### 示例

```javascript
const { exec } = require('child_process');
const command = 'ls -al /';
const child_p = exec(command);
child_p.on('error', (error) => {
    console.log('Child Process on error: ', error);
});
```

## exit

### 事件触发条件

子进程结束时触发, 不论正常结束还是异常结束亦或者是中断结束, 均触发

### 回调函数

exit事件回调函数包含以下2个参数:

- code: Number|null, 进程退出状态码, 如果子进程正常退出, code即为进程的最终退出状态码, 否则该参数值为null
- signal: Node.Signa|null, 进程中断信号, 如果子进程由于接收到中断信号退出, signal即为收到的中断信号

code和signal参数是互斥的, 总是有一个为非空的

!> 注意: 当触发exit事件时, 子进程的stdio流是有可能仍然出于打开的状态, 此时是不会触发 [close](#close) 事件的

### 示例

```javascript
const { exec } = require('child_process');
const command = 'ls -al /';
const child_p = exec(command);
child_p.on('exit', (code, signal) => {
    console.log('Child Process on exit: ', { code, signal });
});
```

## message

### 事件触发条件

主进程或子进程通过 [send()](/repository/Languages/JavaScript/docs/ChildProcessAPI.md#subprocesssendmessage-sendhandle-options-callback) 函数发送进程间通信消息时触发

### 回调函数

message事件回调函数包含以下2个参数:

- message: Object|String|any, 自动反序列化后的进程间通信消息
- sendHandle: Socket, net.Socket 或 net.Server对象或undefined

!> 注意: 进程间通信消息会经过自动的序列化和反序列化转换, 所以在回调函数中接收到的反序列化后的内容*可能*与消息发送方发送的原始内容存在不同, 尤其是设置了可选参数 { serialization: 'advanced' } 时, 该高级序列化格式因为不是JSON的超集, 存在可能的类型兼容问题, 会导致部分消息属性经过序列化处理后属性丢失或结构变化.

### 示例

```javascript
const { exec } = require('child_process');
const command = 'ls -al /';
const child_p = exec(command);
child_p.on('message', (message, handle) => {
    console.log('Child Process on message: ', { message, handle });
});
```

## spawn

### 事件触发条件

子进程派生成功时触发**一次**, 如果子进程派生失败, spawn事件是不会触发的, 取而代之, 一个[error](#error)事件会被触发

?> spawn事件总是会在其他可触发事件前最先触发

!> 注意: spawn事件只会在派生子进程成功后触发一次, 如果设置了可选参数: { shell: true }, 那么子进程会先创建Shell, 再将需要执行的命令交给Shell去执行, 只要Shell的创建是成功的, 就意味着子进程派生成功, 此时spawn事件就会触发, 不论传递给Shell的命令是否开始执行, 执行成功与否, 因此并不能简单的以spawn事件是否触发来判断子进程是否成功的完成派生.

### 回调函数

spawn事件回调函数没有参数

### 示例

```javascript
const { exec } = require('child_process');
const command = 'ls -al /';
const child_p = exec(command);
child_p.on('spawn', () => {
    console.log('Child Process on spawn');
});
```

## stdio.data

此为子进程stdio的事件, stdin, stdout, stderr 均支持

### 事件触发条件

当流释放数据片段所有权时触发

### 回调函数

stdio.data 事件回调函数包含1个参数:

- chunk: Buffer|String, 流释放的数据片段

### 示例

```javascript
const { spawn } = require('child_process');
const command = 'ls';
const args = [ '-al', '/' ];
const child_p = spawn(command, args);
child_p.stdout.on('data', (chunk) => {
    console.log('Child Process stdout on data: ', { data: data.toString() });
});
```

## stdio.close

此为子进程stdio事件, stdin, stdout, stderr 均支持

### 事件触发条件

当流关闭时触发

### 回调函数

stdio.close事件回调函数没有参数

### 示例

```javascript
const { spawn } = require('child_process');
const command = 'ls';
const args = [ '-al', '/' ];
const child_p = spawn(command, args);
child_p.stdout.on('close', () => {
    console.log('Child Process stdout on close');
});
```

## stdio.end

此为子进程stdio事件, stdin, stdout, stderr 均支持

### 事件触发条件

当流关中没有可消费数据时触发

### 回调函数

stdio.end事件回调函数没有参数

### 示例

```javascript
const { spawn } = require('child_process');
const command = 'ls';
const args = [ '-al', '/' ];
const child_p = spawn(command, args);
child_p.stdout.on('end', () => {
    console.log('Child Process stdout on end');
});
```

## stdio.error

此为子进程stdio事件, stdin, stdout, stderr 均支持

### 事件触发条件

满足以下条件之一时触发

- 底层流由于内部异常/故障无法生成数据
- 流送入了无效数据块

### 回调函数

stdio.error事件回调包含1个参数:

- error: Error, 异常错误对象

### 示例

```javascript
const { spawn } = require('child_process');
const command = 'ls';
const args = [ '-al', '/' ];
const child_p = spawn(command, args);
child_p.stdout.on('error', (error) => {
    console.log('Child Process stdout on error: ', error);
});
```