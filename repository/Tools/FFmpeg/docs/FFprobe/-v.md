# -v

---

## 作用

设置输入日志级别

## 用法

```bash
-v <logLevel>
```

LogLevel 参数的值为以下枚举值之一, 命令中可以使用枚举名称也可以使用枚举名称对应的值:

- quiet, -8
- panic, 0
- fatal, 8
- error, 16
- warning, 24
- info, 32
- verbose, 40
- debug, 48
- trace, 56

从上往下, 值越大, 日志输出级别越低, 相同的命令参数, 输出的日志内容越多

默认值: info | 32

## 示例

```bash
ffprobe -v quiet
```
