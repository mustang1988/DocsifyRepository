# -g

---

## 作用

设置视频流的GOP(Group Of Pictures), 即从前一个I帧到下一个I帧之间的帧数


## 用法

```bash
-g <gop>
```

默认值: 12

取值范围: (INT_MIN, INT_MAX)

## 示例

```bash
ffmpeg -g 10
```
