# -pix_fmt

---

## 作用

设置视频流像素格式


## 用法

```shell
-pix_fmt <format>
```

FFmpeg根据编译参数的不同, 对像素格式的支持也不尽相同, 可以使用以下FFmpeg命令, 查看当前所使用的FFmpeg支持的像素格式列表

```shell
ffmpeg -pix_fmts
```

## 示例

```shell
ffmpeg -pix_fmt yuv420p
```
