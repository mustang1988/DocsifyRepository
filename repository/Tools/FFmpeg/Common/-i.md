# -i

---

## 作用

指定FFmpeg的输入内容

输入内容可以是
- 文件
- 流媒体
- 源

## 用法

```bash
-i <input>
```

## 示例

- 文件

```bash
ffmpeg -i test.mp4
```

- 流媒体

```bash
# HLS 流
ffmpeg -i https://www.xxx.com/xxx.m3u8
# RTMP 流
ffmpeg -i rtmp://xxx.xxx.xxx:1935/xxx/xxx
```

- 源

```bash
ffmpeg -i nullsrc=size=640x480
```