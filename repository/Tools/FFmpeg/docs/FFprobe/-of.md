# -of

---

## 作用

设置输出格式

## 用法

```bash
-of <format>
```

PrintFormat 参数的值为以下枚举值之一

### default

此为FFprobe输出的**默认格式**, 输出样式大致如下:

```bash
[FORMAT]
filename=output.mp4
nb_streams=1
nb_programs=0
format_name=mov,mp4,m4a,3gp,3g2,mj2
format_long_name=QuickTime / MOV
start_time=0.000000
duration=10.234000
size=15797948
bit_rate=12349382
probe_score=100
TAG:major_brand=isom
TAG:minor_version=512
TAG:compatible_brands=isomiso2avc1mp41
TAG:encoder=Lavf59.10.100
[/FORMAT]
```

default输出格式有以下可选参数:

#### nokey, nk

设置是否输出属性字段的名称, 即是否输出 [示例](#default) 中属性列表中"="及其前面的部分, 可选值: 0 | 1, 默认值: 0, 0为**输出**字段名称, 1为**不输出**字段名称

示例:

```bash
ffprobe -of default=nk=1
# or
ffprobe -of default=nokey=1
```

输出示例:

```bash
[FORMAT]
output.mp4
1
0
mov,mp4,m4a,3gp,3g2,mj2
QuickTime / MOV
0.000000
10.234000
15797948
12349382
100
isom
512
isomiso2avc1mp41
Lavf59.10.100
[/FORMAT]
```

#### noprint_wrappers, nw

设置是否输出属性分类名称, 即设置是否输出 [示例](#default) 中, "[FORMAT]" 和 "[/FORMAT]" 所在的行, 可选值: 0 | 1, 默认值: 0, 0为**输出**属性分类名称, 1为**不输出**属性分类名称

示例:

```bash
ffprobe -of default=noprint_wrappers=1
# or
ffprobe -of default=nw=1
```

输出示例:

```bash
filename=output.mp4
nb_streams=1
nb_programs=0
format_name=mov,mp4,m4a,3gp,3g2,mj2
format_long_name=QuickTime / MOV
start_time=0.000000
duration=10.234000
size=15797948
bit_rate=12349382
probe_score=100
TAG:major_brand=isom
TAG:minor_version=512
TAG:compatible_brands=isomiso2avc1mp41
TAG:encoder=Lavf59.10.100
```

### csv

csv输出格式大致如下:

```bash
format,output.mp4,1,0,"mov,mp4,m4a,3gp,3g2,mj2",QuickTime / MOV,0.000000,10.234000,15797948,12349382,100,isom,512,isomiso2avc1mp41,Lavf59.10.100
```

csv输出格式有以下可选参数:

#### item_sep, s
#### nokey, nk
#### escape, e
#### print_section, p

### flat

flat输出格式大致如下:

```bash
format.filename="output.mp4"
format.nb_streams=1
format.nb_programs=0
format.format_name="mov,mp4,m4a,3gp,3g2,mj2"
format.format_long_name="QuickTime / MOV"
format.start_time="0.000000"
format.duration="10.234000"
format.size="15797948"
format.bit_rate="12349382"
format.probe_score=100
format.tags.major_brand="isom"
format.tags.minor_version="512"
format.tags.compatible_brands="isomiso2avc1mp41"
format.tags.encoder="Lavf59.10.100"
```

flat输出格式有以下可选参数:

#### sep_char, s
#### hierarchical, h

### ini

ini输出格式大致如下:

```bash
# ffprobe output

[format]
filename=output.mp4
nb_streams=1
nb_programs=0
format_name=mov,mp4,m4a,3gp,3g2,mj2
format_long_name=QuickTime / MOV
start_time=0.000000
duration=10.234000
size=15797948
bit_rate=12349382
probe_score=100

[format.tags]
major_brand=isom
minor_version=512
compatible_brands=isomiso2avc1mp41
encoder=Lavf59.10.100
```

ini输出格式有以下可选参数:

#### hierarchical, h


### json

json输出格式大致如下:

```bash
{
    "format": {
        "filename": "output.mp4",
        "nb_streams": 1,
        "nb_programs": 0,
        "format_name": "mov,mp4,m4a,3gp,3g2,mj2",
        "format_long_name": "QuickTime / MOV",
        "start_time": "0.000000",
        "duration": "10.234000",
        "size": "15797948",
        "bit_rate": "12349382",
        "probe_score": 100,
        "tags": {
            "major_brand": "isom",
            "minor_version": "512",
            "compatible_brands": "isomiso2avc1mp41",
            "encoder": "Lavf59.10.100"
        }
    }
}
```

json输出格式包含以下可选参数:

#### compact, c

设置是否压缩json输出信息, 即将输出的json数据中的换行, 空格等空白字符进行压缩去除, 减小输出体积, 可选值: 0 | 1, 默认值: 0, 0为**不压缩**输出信息, 1为**压缩**输出信息

示例:

```bash
ffprobe -of json=c=1
# or
ffprobe -of json=compact=1
```

输出示例:

```bash
{
    "format": { "filename": "output.mp4", "nb_streams": 1, "nb_programs": 0, "format_name": "mov,mp4,m4a,3gp,3g2,mj2", "format_long_name": "QuickTime / MOV", "start_time": "0.000000", "duration": "10.234000", "size": "15797948", "bit_rate": "12349382", "probe_score": 100,
        "tags": { "major_brand": "isom", "minor_version": "512", "compatible_brands": "isomiso2avc1mp41", "encoder": "Lavf59.10.100" } }
}
```

### xml

xml输出格式大致如下:

```bash
<?xml version="1.0" encoding="UTF-8"?>
<ffprobe>
    <format filename="output.mp4" nb_streams="1" nb_programs="0" format_name="mov,mp4,m4a,3gp,3g2,mj2" format_long_name="QuickTime / MOV" start_time="0.000000" duration="10.234000" size="15797948" bit_rate="12349382" probe_score="100">
        <tag key="major_brand" value="isom"/>
        <tag key="minor_version" value="512"/>
        <tag key="compatible_brands" value="isomiso2avc1mp41"/>
        <tag key="encoder" value="Lavf59.10.100"/>
    </format>
</ffprobe>
```

xml输出格式有以下可选参数:

#### fully_qualified, q
#### xsd_compliant, x


## 示例

```bash
ffprobe -of json
```
