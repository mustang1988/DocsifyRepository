# -c:a

---

## 作用

设置音频流编码器

## 用法

```bash
-c:a <codec>
```

codec为编码器名称, 如果指定编码器, 则FFmpeg会对采用给定的编码器对音频流进行重新编码, 如果不需要重新编码音频流, codec参数可以设置为"copy"

## 示例

```bash
ffmpeg -c:a copy
```
