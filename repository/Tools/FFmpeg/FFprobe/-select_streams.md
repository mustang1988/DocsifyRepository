# -select_streams

---

## 作用

选择输出指定的流信息

## 用法

```shell
-select_streams <stream_specifier>
```

流指定可选值
- v

    视频流

- a

    音频流

- s

    字幕流

- d

    数据流

## 示例

```shell
ffprobe -select_streams a
```
