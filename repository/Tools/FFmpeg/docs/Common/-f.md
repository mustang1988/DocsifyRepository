# -f

---

## 作用

指定格式, 可以是
- 输入格式
- 输出格式


## 用法

```bash
-f <format>
```

## 示例

- 输入格式

```bash
ffmpeg -i input.mp4 -f mp4
```

- 输出格式

```bash
ffmpeg -i input.mp4 -c:v libvpx-vp9 -f webm output.webm
```
