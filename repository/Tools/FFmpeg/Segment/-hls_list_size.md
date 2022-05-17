# -hls_list_size

---

## 作用

设置HLS分片数量

## 用法

```bash
-hls_list_size <int>
```

默认值: 5

取值范围: [0, INT_MAX)

设置值为0时, 为不限制分片数量

## 示例

```bash
ffmpeg -hls_list_size 4
```
