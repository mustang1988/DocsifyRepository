# -c:v

---

## 作用

设置输出视频流的编码器


## 用法

```shell
-c:v <codec>
```

codec为编码器名称, 如果指定编码器, 则FFmpeg会对采用给定的编码器对视频流进行重新编码, 如果不需要重新编码视频流, codec参数可以设置为"copy"

## 示例

```shell
ffmpeg -c:v libx264
```
