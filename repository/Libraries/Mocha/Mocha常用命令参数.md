# Mocha常用命令参数

---

- --allow-uncaught

    - 作用

        禁用自动异常捕获

    - 默认值

        false

- --async-only, -A

    - 作用

        强制使用异步风格编写测试

    - 默认值

        false

- --bail, -b

    - 作用

        运行单元测试时, 当遇到第一个fail的测试用例后, 终止测试

    - 默认值

        false

- --slow <ms>, -s <ms>

    - 作用

        定义"慢"执行的阈值(毫秒数)

- --timeout <ms>, -t <ms>

    - 作用

        测试超时阈值(毫秒数)

    - 默认值

        2000