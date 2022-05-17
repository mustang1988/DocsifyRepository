# -preset

---

## 作用

设置 H.264, H.265(HEVC) 编码器的编码预设


## 用法

```shell
-preset <preset>
```

H.264, H.265(HEVC)提供了以下几个可选预设值
- ultrafast
- superfast
- veryfast
- faster
- fast
- medium
- slow
- slower
- veryslow
- placebo

上述可选预设值从上至下
- 编码速度依次递减
- 编码质量依次降低
- 采用相同编码参数的情况下, 最终编码得到的文件体积依次减小

默认值为: medium

## 示例

```shell
ffmpeg -preset ultrafast
```
