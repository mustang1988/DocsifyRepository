# H.264视频转码后画面失真问题研究

---

## 问题现象

在使用H.264(libx264)编码, 将一个较高码率的原始视频转码为较低码率的页面可播放版本时, 可能出现画面失真的现象

## 问题复现步骤

1. 准备问题复现用文件

  可以复现问题的高码率原始视频文件, 下载地址: TODO(文件丢了, 待重传...)

  原始文件信息如下

  ```json
  {
    "streams": [
      {
        "index": 0,
        "codec_name": "h264",
        "codec_long_name": "H.264 / AVC / MPEG-4 AVC / MPEG-4 part 10",
        "profile": "High",
        "codec_type": "video",
        "codec_tag_string": "avc1",
        "codec_tag": "0x31637661",
        "width": 2560,
        "height": 1440,
        "coded_width": 2560,
        "coded_height": 1440,
        "closed_captions": 0,
        "has_b_frames": 0,
        "sample_aspect_ratio": "1:1",
        "display_aspect_ratio": "16:9",
        "pix_fmt": "yuv420p",
        "level": 51,
        "color_range": "tv",
        "color_space": "smpte170m",
        "color_transfer": "bt470m",
        "color_primaries": "smpte170m",
        "chroma_location": "left",
        "refs": 1,
        "is_avc": "true",
        "nal_length_size": "4",
        "r_frame_rate": "60000/1001",
        "avg_frame_rate": "70470000/1175507",
        "time_base": "1/90000",
        "start_pts": 0,
        "start_time": "0.000000",
        "duration_ts": 1175507,
        "duration": "13.061189",
        "bit_rate": "50229482",
        "bits_per_raw_sample": "8",
        "nb_frames": "783",
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
          "timed_thumbnails": 0
        },
        "tags": {
          "creation_time": "2020-10-12T13:43:40.000000Z",
          "language": "und",
          "handler_name": "VideoHandle",
          "vendor_id": "[0][0][0][0]"
        }
      },
      {
        "index": 1,
        "codec_name": "aac",
        "codec_long_name": "AAC (Advanced Audio Coding)",
        "codec_type": "audio",
        "codec_tag_string": "mp4a",
        "codec_tag": "0x6134706d",
        "sample_fmt": "fltp",
        "sample_rate": "48000",
        "channels": 2,
        "channel_layout": "stereo",
        "bits_per_sample": 0,
        "r_frame_rate": "0/0",
        "avg_frame_rate": "0/0",
        "time_base": "1/48000",
        "start_pts": 0,
        "start_time": "0.000000",
        "duration_ts": 626928,
        "duration": "13.061000",
        "bit_rate": "195475",
        "nb_frames": "605",
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
          "timed_thumbnails": 0
        },
        "tags": {
          "creation_time": "2020-10-12T13:43:40.000000Z",
          "language": "und",
          "handler_name": "SoundHandle",
          "vendor_id": "[0][0][0][0]"
        }
      }
    ],
    "format": {
      "filename": "test_fps_59.94_010.mp4",
      "nb_streams": 2,
      "nb_programs": 0,
      "format_name": "mov,mp4,m4a,3gp,3g2,mj2",
      "format_long_name": "QuickTime / MOV",
      "start_time": "0.000000",
      "duration": "13.061000",
      "size": "82335581",
      "bit_rate": "50431410",
      "probe_score": 100,
      "tags": {
        "major_brand": "mp42",
        "minor_version": "0",
        "compatible_brands": "isommp42",
        "creation_time": "2020-10-12T13:43:40.000000Z",
        "date": "2020"
      }
    }
  }
  ```

2. 将文件转码为页面video标签可播放版本

  使用命令如下

```bash
ffmpeg \
-i test_fps_59.94_010.mp4 \
-c:v libx264 \
-c:a aac \
-r 60000/1001 \
-pix_fmt yuv420p \
-b:v 5M \
-preset ultrafast \
-y \
-f mp4 \
test_fps_59.94_010.video_rate_5M.mp4
```

  转码输出文件信息如下

  ```json
  {
    "streams": [
      {
        "index": 0,
        "codec_name": "h264",
        "codec_long_name": "H.264 / AVC / MPEG-4 AVC / MPEG-4 part 10",
        "profile": "Constrained Baseline",
        "codec_type": "video",
        "codec_tag_string": "avc1",
        "codec_tag": "0x31637661",
        "width": 2560,
        "height": 1440,
        "coded_width": 2560,
        "coded_height": 1440,
        "closed_captions": 0,
        "has_b_frames": 0,
        "sample_aspect_ratio": "1:1",
        "display_aspect_ratio": "16:9",
        "pix_fmt": "yuv420p",
        "level": 51,
        "color_range": "tv",
        "color_space": "smpte170m",
        "color_transfer": "bt470m",
        "color_primaries": "smpte170m",
        "chroma_location": "left",
        "refs": 1,
        "is_avc": "true",
        "nal_length_size": "4",
        "r_frame_rate": "60000/1001",
        "avg_frame_rate": "60000/1001",
        "time_base": "1/60000",
        "start_pts": 0,
        "start_time": "0.000000",
        "duration_ts": 783783,
        "duration": "13.063050",
        "bit_rate": "5342474",
        "bits_per_raw_sample": "8",
        "nb_frames": "783",
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
          "timed_thumbnails": 0
        },
        "tags": {
          "language": "und",
          "handler_name": "VideoHandle",
          "vendor_id": "[0][0][0][0]"
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
        "sample_rate": "44100",
        "channels": 2,
        "channel_layout": "stereo",
        "bits_per_sample": 0,
        "r_frame_rate": "0/0",
        "avg_frame_rate": "0/0",
        "time_base": "1/44100",
        "start_pts": 0,
        "start_time": "0.000000",
        "duration_ts": 569993,
        "duration": "12.925011",
        "bit_rate": "128269",
        "nb_frames": "557",
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
          "timed_thumbnails": 0
        },
        "tags": {
          "language": "und",
          "handler_name": "SoundHandle",
          "vendor_id": "[0][0][0][0]"
        }
      }
    ],
    "format": {
      "filename": "test_fps_59.94_010.video_rate_5M.mp4",
      "nb_streams": 2,
      "nb_programs": 0,
      "format_name": "mov,mp4,m4a,3gp,3g2,mj2",
      "format_long_name": "QuickTime / MOV",
      "start_time": "0.000000",
      "duration": "13.064000",
      "size": "8951018",
      "bit_rate": "5481333",
      "probe_score": 100,
      "tags": {
        "major_brand": "isom",
        "minor_version": "512",
        "compatible_brands": "isomiso2avc1mp41",
        "date": "2020",
        "encoder": "Lavf58.76.100"
      }
    }
  }
  ```

3. 播放转码输出文件

  会发现视频中存在大量马赛克般的噪点, 画面闪烁不清晰

## 问题出现原因分析

H.264 编码算法在码率压缩时, 因为算法本身的压缩率不够高, 会丢失大量细节信息, 在分辨率保持不变的前提下, 码率下降越多, 转码输出文件的视觉效果越差

## 解决方案

改用对码率压缩效率更高的VP9编码器对文件进行转码

转码命令如下

```bash
ffmpeg \
-i test_fps_59.94_010.mp4 \
-c:v libvpx-vp9 \
-c:a libopus \
-r 60000/1001 \
-pix_fmt yuv420p \
-b:v 5M \
-quality best \
-speed 16 \
-deadline realtime \
-f webm \
-y \
test_fps_59.94_010.vp9.video_rate_5M.webm
```

转码输出文件信息如下

```json
{
  "streams": [
    {
      "index": 0,
      "codec_name": "vp9",
      "codec_long_name": "Google VP9",
      "profile": "Profile 0",
      "codec_type": "video",
      "codec_tag_string": "[0][0][0][0]",
      "codec_tag": "0x0000",
      "width": 2560,
      "height": 1440,
      "coded_width": 2560,
      "coded_height": 1440,
      "closed_captions": 0,
      "has_b_frames": 0,
      "sample_aspect_ratio": "1:1",
      "display_aspect_ratio": "16:9",
      "pix_fmt": "yuv420p",
      "level": -99,
      "color_range": "tv",
      "color_space": "smpte170m",
      "color_transfer": "bt470m",
      "color_primaries": "smpte170m",
      "chroma_location": "left",
      "field_order": "progressive",
      "refs": 1,
      "r_frame_rate": "19001/317",
      "avg_frame_rate": "19001/317",
      "time_base": "1/1000",
      "start_pts": 7,
      "start_time": "0.007000",
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
        "timed_thumbnails": 0
      },
      "tags": {
        "HANDLER_NAME": "VideoHandle",
        "VENDOR_ID": "[0][0][0][0]",
        "ENCODER": "Lavc58.134.100 libvpx-vp9",
        "DURATION": "00:00:13.070000000"
      }
    },
    {
      "index": 1,
      "codec_name": "opus",
      "codec_long_name": "Opus (Opus Interactive Audio Codec)",
      "codec_type": "audio",
      "codec_tag_string": "[0][0][0][0]",
      "codec_tag": "0x0000",
      "sample_fmt": "fltp",
      "sample_rate": "48000",
      "channels": 2,
      "channel_layout": "stereo",
      "bits_per_sample": 0,
      "r_frame_rate": "0/0",
      "avg_frame_rate": "0/0",
      "time_base": "1/1000",
      "start_pts": -7,
      "start_time": "-0.007000",
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
        "timed_thumbnails": 0
      },
      "tags": {
        "HANDLER_NAME": "SoundHandle",
        "VENDOR_ID": "[0][0][0][0]",
        "ENCODER": "Lavc58.134.100 libopus",
        "DURATION": "00:00:12.932000000"
      }
    }
  ],
  "format": {
    "filename": "test_fps_59.94_010.vp9.video_rate_5M.webm",
    "nb_streams": 2,
    "nb_programs": 0,
    "format_name": "matroska,webm",
    "format_long_name": "Matroska / WebM",
    "start_time": "-0.007000",
    "duration": "13.070000",
    "size": "17103848",
    "bit_rate": "10469072",
    "probe_score": 100,
    "tags": {
      "DATE": "2020",
      "MAJOR_BRAND": "mp42",
      "MINOR_VERSION": "0",
      "COMPATIBLE_BRANDS": "isommp42",
      "ENCODER": "Lavf58.76.100"
    }
  }
}
```

播放该输出文件, 画面马赛克和噪点明显减少, 质量提升很明显

## VP9解决方案存在的缺点

1. 转码速度较慢

  VP9编码时, 可以通过设置 -deadaline, -speed, -quality, -cpu-used 等参数调整转码速度, 但实测后发现, 效果有限, 转码的速度上与H.264还是存在一些差距, 转码的时间成本相对较高.

2. 页面video标签的播放兼容性相对略差

  因为改用了VP9编码器编码, 对非Google WebKit内核的浏览器兼容性存在问题, 可以支持的浏览器覆盖面要比H.264编码来的少.

## 总结

- 如果有将高码率视频进行大幅度码率压缩的需求, 不建议使用H.264编码, 码率压低后画质会很惨 /(ㄒoㄒ)/~~
- 如果对浏览器兼容性不是太敏感的应用, 建议使用VP9编码器对视频编码

## 扩展

使用VP9编码器可以解决码率压缩导致的画面问题, 原因是VP9编码器有更高的低码率压缩支持, 那么为什么不使用码率压缩更高的HEVC(H.265)编码器呢?

核心原因:

目前主流浏览器都还不支持在页面上直接解码播放

如果希望在页面上直接解码播放HEVC编码的视频文件, 现阶段是可以通过将HEVC解码以WebAssamblly组件的方式加入到页面中实现

但是, 视频的解码需要依靠客户机的CPU或GPU来完成, 而HEVC的解码是很吃硬件配置的, 英特尔第八代酷睿和AMD Ryzen及其之后上市的CPU才有硬件HEVC的解码支持, 此前的CPU是没有硬件加速支持的, 只能依赖CPU算力进行软解码

实测通过WASM方式将FFmpeg接入到页面中实现解码播放720p的HEVC视频文件, 在4代i7的配置下(Macbook 2015), 播放时CPU占用率可以达到100%, 而画面播放依旧会出现明显的卡顿, 因此, 目前WASM方式在页面播放HEVC视频还出于试验阶段, 基本不可用于实际生产环境中

基于上述原因, 同时考虑到硬件兼容性, 软件兼容性和码率压缩后的画面观感, 使用VP9编码器来编码在页面上直接播放的视频文件, 是一个比较好的折中选择