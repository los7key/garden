---
layout: post
title: Convert mp4 to gif
description: Convert mp4 to gif
date: 2022-04-26
Last Updated: 2023-03-12
---
## Requirements 
* youtube-dl (brew)
* ffmpeg (brew)

## Gif Magic
1. Get list of available formats: `youtube-dl -F "https://www.youtube.com/watch?v=0N-nX_4C95o"`
2. Download: `youtube-dl -f 134 "https://www.youtube.com/watch?v=0N-nX_4C95o"`
3. If needed convert to mp4: `ffmpeg -i Huna.webm -strict experimental Huna.Timelapse.mp4`
4. Trim with iMovie
5. Encode mp4 to gif: `./gifenc.sh chimpscropped.mp4 chimps.gif`

```
$ cat gifenc.sh
#!/bin/sh
#
# USAGE: ./gifenc.sh input.mov output.gif 720 10 will output 720p wide 10fps GIF from the movie you gave it.
# https://cassidy.codes/blog/2017/04/25/ffmpeg-frames-to-gif-optimization/
#
# Vars
fps=10
scl=720
palette="/tmp/palette.png"
filters="fps=$fps,scale=$scl:-1:flags=lanczos"

##ffmpeg -v warning -i "$1" -vf "$filters,palettegen" -y "$palette"
##ffmpeg -v warning -i "$1" -i $palette -lavfi "$filters [x]; [x][1:v] paletteuse" -y "$2"

ffmpeg -v warning -i $1 -vf "$filters,palettegen=stats_mode=diff" -y $palette
ffmpeg -i $1 -i $palette -lavfi "$filters,paletteuse=dither=bayer:bayer_scale=5:diff_mode=rectangle" -y $2
```

To take every 15th frame, use
```
ffmpeg -i in.mp4 -vf select='not(mod(n,15))',setpts=N/FRAME_RATE/TB out.mp4
```

Another method is to use the framestep filter
```
ffmpeg -i in.mp4 -vf framestep=15,setpts=N/FRAME_RATE/TB out.mp4
```

## More ffmpeg commands

Join audio files 

The loop puts all the filenames in a file, one-per-line, then uses ffmpeg's concat demuxer to merge the files
```
for f in *.flac; do echo "file '$f'" >> inputs.txt; done
ffmpeg -f concat -i inputs.txt 
```

Convert to MP4
```
ffmpeg -i $input_file.mkv -codec copy $output_file.mp4
```

Combine video and audio with an offset
```
ffmpeg -i $input_file.mp4 -itsoffset 00:00:08 -i $input_file.mp3 output.mp4
```

Remove audio from a video 
```
ffmpeg -i $input_file -c copy -an $output_file
```

## References 

https://www.expertstool.com/linkedin-video-downloader/ (for LI videos)
