# FFmpeg创建纯色视频文件

---

## 命令格式与示例

```bash
ffmpeg \
-ss 0 \
-t <duration> \
-f lavfi \
-i color=c=<color>:s=<resolutuion>:r=<fps> \
-c:v <codec> \
-f <format> \
<output>
```

示例:

```bash
# 创建一个时长30秒, 分辨率1920x1080, 帧率60, 颜色为纯红RGB(255,0,0)的视频, 文件名为Red.mp4
ffmpeg \
-ss 0 \
-t 30 \
-f lavfi \
-i color=c=0xff0000:s=1920x1080:r=60 \
-c:v libx264 \
-r:v 60 \
-f mp4 \
Red.mp4
```

## 参数说明

|||
|:-|:-|
|duration|创建的视频时长, 单位: 秒|
|color|纯色视频画面颜色, 16进制RGB色值, 0x开头|
|resolutuion|画面分辨率, 格式为宽度x高度, 单位: 像素|
|fps|画面帧率|
|codec|视频编码器|
|format|输出文件格式|
|output|输出文件路径|