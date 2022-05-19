# Mocha对TypeScript执行单元测试

---

## 安装ts-node

```bash
npm i ts-node -D
```

ts-node 是一个可以在NodeJS环境下直接运行TypeScript代码而不需要事先将TypeScript源码编译成JavaScript的工具

## 为Mocha配置ts-node

编辑package.json, 在启动mocha测试的命令中, 加入ts-node

> mocha ts-node/register ...

## 直接使用TypeScript编写Mocha测试用例

```typescript

import { describe, it } from 'mocha'
import assert from 'assert'

describe('xxx.ts', () => {
    it('xxx', () => {
        // 一般测试用例
    });

    it('xxx', (done) => {
        // Promise测试用例
    });

});
```