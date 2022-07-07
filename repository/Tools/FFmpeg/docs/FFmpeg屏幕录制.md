# FFmpeg屏幕录制

---

## Windows下使用FFmpeg进行屏幕录制

命令格式:

```bash
ffmpeg \
-f gdigrab \
-r <fps> \
-i desktop \
<output>
```

参数说明:

|参数|说明|备注|
|:-|:-|:-|
|fps|录制帧率|数值或帧率比值|
|output|输出|输出文件或输出流地址|