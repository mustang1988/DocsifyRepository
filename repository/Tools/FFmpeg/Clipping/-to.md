# -to

---

## 作用

设置剪辑结束点, 单位 秒

!> 需要注意, 实际使用该参数进行剪辑时, 如果指定的结束点不是I帧, 则FFmpeg会在剪辑结束点后最近的I帧处结束

## 用法

```bash
-to <time_stop>
```

## 示例

```bash
ffmpeg -to 7
```