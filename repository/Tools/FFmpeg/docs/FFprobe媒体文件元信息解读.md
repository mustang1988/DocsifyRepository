# FFprobe媒体文件元信息解读

---

获取测试用媒体文件: [下载地址](https://4kmedia.org/sony-swordsmith-hdr-uhd-4k-demo/), 下载后重命名媒体文件为: Swordsmith.mp4

使用ffprobe通过以下参数读取媒体文件元信息

```bash
ffprobe -v 0 -of json -show_streams -show_format -i Swordsmith.mp4
```

得到输出的元信息如下: 

```json
{
    "streams": [
        {
            "index": 0,
            "codec_name": "hevc",
            "codec_long_name": "H.265 / HEVC (High Efficiency Video Coding)",
            "profile": "Main 10",
            "codec_type": "video",
            "codec_tag_string": "hvc1",
            "codec_tag": "0x31637668",
            "width": 3840,
            "height": 2160,
            "coded_width": 3840,
            "coded_height": 2160,
            "closed_captions": 0,
            "film_grain": 0,
            "has_b_frames": 1,
            "sample_aspect_ratio": "1:1",
            "display_aspect_ratio": "16:9",
            "pix_fmt": "yuv420p10le",
            "level": 153,
            "color_range": "tv",
            "color_space": "bt2020nc",
            "color_transfer": "smpte2084",
            "color_primaries": "bt2020",
            "chroma_location": "topleft",
            "refs": 1,
            "id": "0x1",
            "r_frame_rate": "60000/1001",
            "avg_frame_rate": "60000/1001",
            "time_base": "1/60000",
            "start_pts": 0,
            "start_time": "0.000000",
            "duration_ts": 5165160,
            "duration": "86.086000",
            "bit_rate": "71382367",
            "nb_frames": "5160",
            "extradata_size": 150,
            "disposition": {
                "default": 1,
                "dub": 0,
                "original": 0,
                "comment": 0,
                "lyrics": 0,
                "karaoke": 0,
                "forced": 0,
                "hearing_impaired": 0,
                "visual_impaired": 0,
                "clean_effects": 0,
                "attached_pic": 0,
                "timed_thumbnails": 0,
                "captions": 0,
                "descriptions": 0,
                "metadata": 0,
                "dependent": 0,
                "still_image": 0
            },
            "tags": {
                "creation_time": "2016-10-24T06:29:51.000000Z",
                "language": "und",
                "handler_name": "Video Media Handler",
                "vendor_id": "[0][0][0][0]",
                "encoder": "HEVC Coding"
            }
        },
        {
            "index": 1,
            "codec_name": "aac",
            "codec_long_name": "AAC (Advanced Audio Coding)",
            "profile": "LC",
            "codec_type": "audio",
            "codec_tag_string": "mp4a",
            "codec_tag": "0x6134706d",
            "sample_fmt": "fltp",
            "sample_rate": "48000",
            "channels": 2,
            "channel_layout": "stereo",
            "bits_per_sample": 0,
            "id": "0x2",
            "r_frame_rate": "0/0",
            "avg_frame_rate": "0/0",
            "time_base": "1/48000",
            "start_pts": 0,
            "start_time": "0.000000",
            "duration_ts": 4132864,
            "duration": "86.101333",
            "bit_rate": "192000",
            "nb_frames": "4037",
            "extradata_size": 2,
            "disposition": {
                "default": 1,
                "dub": 0,
                "original": 0,
                "comment": 0,
                "lyrics": 0,
                "karaoke": 0,
                "forced": 0,
                "hearing_impaired": 0,
                "visual_impaired": 0,
                "clean_effects": 0,
                "attached_pic": 0,
                "timed_thumbnails": 0,
                "captions": 0,
                "descriptions": 0,
                "metadata": 0,
                "dependent": 0,
                "still_image": 0
            },
            "tags": {
                "creation_time": "2016-10-24T06:29:51.000000Z",
                "language": "eng",
                "handler_name": "Sound Media Handler",
                "vendor_id": "[0][0][0][0]"
            }
        }
    ],
    "format": {
        "filename": "Swordsmith.mp4",
        "nb_streams": 2,
        "nb_programs": 0,
        "format_name": "mov,mp4,m4a,3gp,3g2,mj2",
        "format_long_name": "QuickTime / MOV",
        "start_time": "0.000000",
        "duration": "86.101333",
        "size": "770255991",
        "bit_rate": "71567392",
        "probe_score": 100,
        "tags": {
            "major_brand": "isom",
            "minor_version": "1",
            "compatible_brands": "isom",
            "creation_time": "2016-10-24T05:33:14.000000Z"
        }
    }
}
```

元信息中包含 streams 和 format 两部分信息, 分别对应媒体文件的流信息和格式信息

## 流信息解读

在解析得到的元信息中, 流信息即为 streams 属性下的信息, 其格式为对象数组, 数组长度为媒体包含的流的数量, 数组中每个元素即为对应流的信息

每个流一定包含有以下2个属性:

### index

值类型为数值, 表示当前流在媒体文件所有流中的索引号, 索引号起始值为0

### codec_type

值类型为字符串, 表示当前流的类型, 常见以下几种值:

- "video", 表示当前流是一个视频流
- "audio", 表示当前流是一个音频流
- "data", 表示当前流是一个数据流
- "subtitle", 表示当前流是一个字幕流

### 视频流信息解读

根据codec_type值, 取出元信息中的视频流部分:

```json
{
    "index": 0,
    "codec_name": "hevc",
    "codec_long_name": "H.265 / HEVC (High Efficiency Video Coding)",
    "profile": "Main 10",
    "codec_type": "video",
    "codec_tag_string": "hvc1",
    "codec_tag": "0x31637668",
    "width": 3840,
    "height": 2160,
    "coded_width": 3840,
    "coded_height": 2160,
    "closed_captions": 0,
    "film_grain": 0,
    "has_b_frames": 1,
    "sample_aspect_ratio": "1:1",
    "display_aspect_ratio": "16:9",
    "pix_fmt": "yuv420p10le",
    "level": 153,
    "color_range": "tv",
    "color_space": "bt2020nc",
    "color_transfer": "smpte2084",
    "color_primaries": "bt2020",
    "chroma_location": "topleft",
    "refs": 1,
    "id": "0x1",
    "r_frame_rate": "60000/1001",
    "avg_frame_rate": "60000/1001",
    "time_base": "1/60000",
    "start_pts": 0,
    "start_time": "0.000000",
    "duration_ts": 5165160,
    "duration": "86.086000",
    "bit_rate": "71382367",
    "nb_frames": "5160",
    "extradata_size": 150,
    "disposition": {
        "default": 1,
        "dub": 0,
        "original": 0,
        "comment": 0,
        "lyrics": 0,
        "karaoke": 0,
        "forced": 0,
        "hearing_impaired": 0,
        "visual_impaired": 0,
        "clean_effects": 0,
        "attached_pic": 0,
        "timed_thumbnails": 0,
        "captions": 0,
        "descriptions": 0,
        "metadata": 0,
        "dependent": 0,
        "still_image": 0
    },
    "tags": {
        "creation_time": "2016-10-24T06:29:51.000000Z",
        "language": "und",
        "handler_name": "Video Media Handler",
        "vendor_id": "[0][0][0][0]",
        "encoder": "HEVC Coding"
    }
}
```

#### codec_name, codec_long_name

视频流编码器的简称与全称

#### width, coded_width, height, coded_height

width, height为视频的宽度和高度, 单位: 像素

coded_width, coded_height为视频的编码宽度和编码高度, 单位: 像素

因为某些编码器对视频流的尺寸有倍数要求, 例如: H.264 编码器, 就要求宽高是16的倍数.

当编码时指定的视频宽高不是编码器要求值的倍数时, 编码器在编码时会将宽高填充到最接近目标宽高值的一个倍数值(不会超过指定的宽高值)进行编码, 并为解码器存储裁剪值, coded_width和coded_height值就是裁剪前的宽高值.

?> 一般情况下, 视频文件的 width和coded_width会是相等的, height和coded_height也会是相等的

#### has_b_frames

解码器中帧重排序缓冲区的大小

可以将此属性理解为视频中的双向预测帧(B帧)向前和向后引用了多少帧的数据, 当此属性值为0时, 意味着视频流中并没有B帧, 只有I帧和P帧.

关于I,P,B帧, 可参考, 10:22 左右开始:

<iframe width="720" height="540" src="//player.bilibili.com/player.html?aid=37424012&bvid=BV1nt411Q7S6&cid=65779111&page=1" scrolling="no" allowfullscreen="true"></iframe>

#### sample_aspect_ratio, display_aspect_ratio

此属性值为字符串格式的比值, 比例分隔符为: ":"

前者为视频流的采样宽高比, 后者为播放时的显示宽高比

#### pix_fmt

**TODO**

#### color_range, color_space, color_transfer 和 color_primaries

这几个属性均用来描述视频色彩范围

**TODO, 涉及HDR和SDR知识点**

#### r_frame_rate, avg_frame_rate

视频流的帧率, 字符串格式的比值, 比例分隔符为: "/"

"xxx/yyy", 表示 yyy 秒内有 xxx 幅画面(帧)

r_frame_rate表示视频的真实帧率, avg_frame_rate为平均帧率

!> 注意: 美制NTSC制式因为某些历史原因([has_b_frames](#has_b_frames)章节视频中有解释)</br>存在一些非整数帧率值, 其中常见的有: 23.976, 29.97, 47.952 和 59.94</br>其对应的帧率, 用比值表示分别为: '24000/1001', '30000/1001', '48000/1001' 和 '60000/1001'</br>在使用FFmpeg进行视频转码时, 注意这些帧率的 [ -r 参数](/repository/Tools/FFmpeg/docs/VideoStream/Common/-r.md#r) 参数不要用小数, 要用比值, 否则转码结果是不正确的.

#### duration

此属性值为数值类型, 表示视频流的时长, 单位: 秒

#### bit_rate

此属性值为数值类型, 表示视频流的码率, 单位: bps

#### nb_frames

此属性值为数值类型, 表示视频流的总帧数

### 音频流信息解读

根据codec_type值, 取出元信息中的音频流部分:

```json
{
    "index": 1,
    "codec_name": "aac",
    "codec_long_name": "AAC (Advanced Audio Coding)",
    "profile": "LC",
    "codec_type": "audio",
    "codec_tag_string": "mp4a",
    "codec_tag": "0x6134706d",
    "sample_fmt": "fltp",
    "sample_rate": "48000",
    "channels": 2,
    "channel_layout": "stereo",
    "bits_per_sample": 0,
    "id": "0x2",
    "r_frame_rate": "0/0",
    "avg_frame_rate": "0/0",
    "time_base": "1/48000",
    "start_pts": 0,
    "start_time": "0.000000",
    "duration_ts": 4132864,
    "duration": "86.101333",
    "bit_rate": "192000",
    "nb_frames": "4037",
    "extradata_size": 2,
    "disposition": {
        "default": 1,
        "dub": 0,
        "original": 0,
        "comment": 0,
        "lyrics": 0,
        "karaoke": 0,
        "forced": 0,
        "hearing_impaired": 0,
        "visual_impaired": 0,
        "clean_effects": 0,
        "attached_pic": 0,
        "timed_thumbnails": 0,
        "captions": 0,
        "descriptions": 0,
        "metadata": 0,
        "dependent": 0,
        "still_image": 0
    },
    "tags": {
        "creation_time": "2016-10-24T06:29:51.000000Z",
        "language": "eng",
        "handler_name": "Sound Media Handler",
        "vendor_id": "[0][0][0][0]"
    }
}
```

#### codec_name, codec_long_name

音频编码器名的简称和全称

#### sample_fmt

音频采样格式

#### sample_rate

音频采样率, 单位: Hz

#### channels

音频通道数量, 单声道为1, 立体声(双声道)为2, 与 [音频声道布局](#channel_layout) 有关

#### channel_layout

音频声道布局

![](../images/audio_channel_layout.png)

常见音频声道布局有以下几种:

- mono:           FC
- stereo:         FL+FR
- 2.1:            FL+FR+LFE
- 3.0:            FL+FR+FC
- 3.0(back):      FL+FR+BC
- 4.0:            FL+FR+FC+BC
- quad:           FL+FR+BL+BR
- quad(side):     FL+FR+SL+SR
- 3.1:            FL+FR+FC+LFE
- 5.0:            FL+FR+FC+BL+BR
- 5.0(side):      FL+FR+FC+SL+SR
- 4.1:            FL+FR+FC+LFE+BC
- 5.1:            FL+FR+FC+LFE+BL+BR
- 5.1(side):      FL+FR+FC+LFE+SL+SR
- 6.0:            FL+FR+FC+BC+SL+SR
- 6.0(front):     FL+FR+FLC+FRC+SL+SR
- hexagonal:      FL+FR+FC+BL+BR+BC
- 6.1:            FL+FR+FC+LFE+BC+SL+SR
- 6.1(back):      FL+FR+FC+LFE+BL+BR+BC
- 6.1(front):     FL+FR+LFE+FLC+FRC+SL+SR
- 7.0:            FL+FR+FC+BL+BR+SL+SR
- 7.0(front):     FL+FR+FC+FLC+FRC+SL+SR
- 7.1:            FL+FR+FC+LFE+BL+BR+SL+SR
- 7.1(wide):      FL+FR+FC+LFE+BL+BR+FLC+FRC
- 7.1(wide-side): FL+FR+FC+LFE+FLC+FRC+SL+SR
- octagonal:      FL+FR+FC+BL+BR+BC+SL+SR
- hexadecagonal:  FL+FR+FC+BL+BR+BC+SL+SR+TFL+TFC+TFR+TBL+TBC+TBR+WL+WR
- downmix:        DL+DR
- 22.2:           FL+FR+FC+LFE+BL+BR+FLC+FRC+BC+SL+SR+TC+TFL+TFC+TFR+TBL+TBC+TBR+LFE2+TSL+TSR+BFC+BFL+BFR

#### bits_per_sample

每个采样点数据比特数量

#### bit_rate

音频码率, 单位: bps

### 数据流信息解读

**TODO**

### 字幕流信息解读

**TODO**

## 格式信息解读

取出元信息中的format部分

```json
{
    "filename": "Swordsmith.mp4",
    "nb_streams": 2,
    "nb_programs": 0,
    "format_name": "mov,mp4,m4a,3gp,3g2,mj2",
    "format_long_name": "QuickTime / MOV",
    "start_time": "0.000000",
    "duration": "86.101333",
    "size": "770255991",
    "bit_rate": "71567392",
    "probe_score": 100,
    "tags": {
        "major_brand": "isom",
        "minor_version": "1",
        "compatible_brands": "isom",
        "creation_time": "2016-10-24T05:33:14.000000Z"
    }
}
```

#### filename

文件路径

#### nb_streams

文件中包含的流数量

#### format_name, format_long_name

封装格式名称的简称和全称

#### start_time

文件开始时间, 单位: 秒

#### duration

文件封装格式时长, 单位: 秒

#### size

文件大小, 单位: Byte

#### probe_score

FFprobe给出的文件信息价值评分

一个输入(在本例中是一个文件)可以有一个扩展名(比如".avi")并且具有不同的格式(例如wav文件), FFmpeg可以检测输入的真实格式(使用ffprobe), 为了做到这一点，它打开文件并读取它(前5秒，如果我没记错的话，由选项analyzeduration设置), 然后，它给每一种格式分配一个分数:如果数据与输入无关，得分较低;如果格式看起来正确，得分较高, 

返回的格式是得分最高的格式, Probe_score是这个分数.

100是最大分数，这意味着FFmpeg确定格式是真实的, 如果评分低于25，则建议增加探测持续时间.