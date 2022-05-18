# -cpu-used

---

## 作用

设置质量/速度比量化器, 该量化器值用于快速设置编码质量与编码速度的权衡关系

## 用法

```bash
-cpu-used <int>
```

默认值: 1

取值范围: [0, 8]

## 示例

```bash
ffmpeg -cpu-used 2
```