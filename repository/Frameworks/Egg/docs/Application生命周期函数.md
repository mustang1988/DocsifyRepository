# Application生命周期函数

---

## 示例

Egg的Application提供生命周期函数的Hook, 可以在app.js或agent.js中自定义处理逻辑, 例如在服务关停时清理服务器缓存, 在服务启动完成后通知其他服务等

[官方参考](https://eggjs.org/zh-cn/advanced/loader.html)

!> 注意: 声明周期函数中, 不建议添加耗时的操作, eggjs对生命周期设有超时处理

示例代码:

```javascript
class AppBootHook {
  constructor(app) {
    this.app = app;
  }

  configWillLoad() {
    
  }

  configDidLoad() {
    
  }

  async didLoad() {
    
  }

  async willReady() {
    
  }

  async didReady() {
    
  }

  async serverDidReady() {
    
  }

  async beforeClose() {
    
  }
}

module.exports = AppBootHook;
```

## 生命周期函数

|函数名|说明|备注|
|:-|:-|:-|
|configWillLoad|配置文件于插件即将完成加载|此时是最后可以动态修改配置信息的地方|
|configDidLoad|配置文件于插件已完成加载||
|didLoad|所有代码文件已完成加载, 正在启动插件||
|willReady|所有插件已完成启动, 服务服务即将启动||
|didReady|所有worker进程已经启动||
|serverDidReady|服务已经完成启动开始监听||
|beforeClose|服务即将关闭|在框架的进程关闭处理中是有超时时间的, 如果 worker 进程在接收到进程退出信号之后, 没有在所规定的时间内退出, 将会被强制关闭*EGG_APP_CLOSE_TIMEOUT*环境变量, 用于设置 app worker 启动超时, *EGG_AGENT_CLOSE_TIMEOUT*环境变量, 用于设置 agent worker 启动超时|

## 在声明周期函数中使用Context上下文对象

可以在生命周期函数中通过*createAnonymousContext()*创建一个匿名Context上下文对象

示例代码:

```javascript
'use strict'
class AppBootHook {
    constructor(app) {
        this.app = app;
    }
    async beforeClose() {
        // mock 一个匿名ctx
        const ctx = await this.app.createAnonymousContext()
        const { service, logger } = ctx
    }
}

module.exports = AppBootHook;
```