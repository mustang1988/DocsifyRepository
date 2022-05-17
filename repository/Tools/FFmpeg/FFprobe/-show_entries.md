# -show_entries

---

## 作用

输出指定字段数据

## 用法

```shell
-show_entries <entry_list>
```

entry_list 格式大致为

<类型1>=<字段名1>,<字段名2>,...:<类型2>=<字段名1>,<字段名2>,...

## 示例

```shell
ffprobe -show_entries streams=index,duration,codec:format=duration,name
```
