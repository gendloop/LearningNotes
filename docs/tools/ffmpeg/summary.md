# Summary

## 视频分段

```bash
# 按 30 min 分段
ffmpeg -i video.mp4 \
      -c copy -map 0 \
      -segment_time 1800 \
      -reset_timestamps 1 \
      -f segment \
      video_%02d.mp4
```

## 截取视频片段

```bash
# 从 1 分钟开始截取, 截取时长为 30 秒
ffmpeg -i input.mp4 \
      -ss 00:01:00 \
      -t 00:00:30 \
      -c copy \
      output.mp4
```

## 合并视频和音频

```bash
# 保持原始音视频编码
ffmpeg -i video.mp4 -i audio.mp3 \
      -c:v copy -c:a copy \
      output.mp4

# 用新的音频替换原有的音频
ffmpeg -i video.mp4 -i audio.mp3 \
      -c:v copy -c:a aac \
      -map 0:v:0 -map 1:a:0 \
      -shortest \
      output.mp4
# -c:v copy    复制视频流
# -c:a aac     将音频转换为 AAC 格式
# -map 0:v:0   选择第一个输入文件的视频流
# -map 1:a:0   选择第二个输入文件的音频流
# -shortest    以较短的输入为准, 避免音频或视频超长

# 音频延迟
ffmpeg -i video.mp4 -i audio.mp3 \
      -filter_complex "[1:a]adelay=1000|1000[delayed];[0:a][delayed]amix=inputs=2[a]" \
      -c:v copy \
      -map 0:v:0 -map "[a]" \
      output.mp4
# adelay=1000|1000 延迟音频 1000 毫秒(左/右声道)
```

## References

1. [http://ffmpeg.org/ffmpeg-all.html#segment_002c-stream_005fsegment_002c-ssegment](http://ffmpeg.org/ffmpeg-all.html#segment_002c-stream_005fsegment_002c-ssegment)
2. [https://ffmpeg.org//ffmpeg-utils.html#time-duration-syntax](https://ffmpeg.org//ffmpeg-utils.html#time-duration-syntax)
3. [https://trac.ffmpeg.org/](https://trac.ffmpeg.org/)
