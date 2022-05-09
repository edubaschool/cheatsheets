### ffmpeg
##### ffmpeg Layout Complet

ffmpeg -y -i 7essai.mkv -i img.png -filter_complex "[1][0]scale2ref[i][m];[m][i]overlay[v]" -map "[v]" -map 0:a? -ac 2 output.mp4 #layout complet

##### ffmpeg mettre une image par dessus une video

ffmpeg -i 7essai.mkv -i test.jpg -filter_complex \
"[0:v][1:v]overlay=900:400:enable=between(t\,0\,30)" -codec:a copy out.mp4 

##### ffmpeg lossless

ffmpeg -video_size 1920x1080 -framerate 30 -f x11grab -i :0.0 -c:v libx264 -crf 0 -preset ultrafast facbookchat.mkv


#### ffmpeg audio et video
ffmpeg -video_size 1366x768 -framerate 25 -f x11grab -i :0.0 -f pulse -ac 2 -i default output.mkv

#### ffmpeg read and list cam devices
ls -ltrh /dev/video*
v4l2-ctl --list-devices

#### ffpmeg list webcam resolution
ffmpeg -f video4linux2 -list_formats all -i /dev/video0

#### ffmpeg record webcam
ffmpeg -f v4l2 -framerate 25 -video_size 640x480 -i /dev/video0 output.mkv

#### ffmpeg record audio sound from computer
ffmpeg -f pulse -i alsa_output.pci-0000_00_1b.0.analog-stereo.monitor cazzo.mp3

##### ffmpeg To take a screenshot screen.png: 
ffmpeg -f x11grab -video_size 1366x768 -i $DISPLAY -vframes 1 screen.png

#### ffmpeg To take a screencast screen.mkv with lossless encoding and without audio: 
ffmpeg -f x11grab -video_size 1366x768 -framerate 25 -i $DISPLAY -c:v ffvhuff screen.mkv

#### ffmpeg To take a screencast screen.mp4 with lossy encoding and with audio: 
ffmpeg -f x11grab -video_size 1366x768 -framerate 25 -i $DISPLAY -f alsa -i default -c:v libx264 -preset ultrafast -c:a aac screen.mp4

#### ffmpeg To record a video webcam.mp4 from the webcam without audio
ffmpeg -f v4l2 -video_size 640x480 -i /dev/video0 -c:v libx264 -preset ultrafast webcam.mp4

##### ffmpeg  To record a video webcam.mp4 from the webcam with audio: 
ffmpeg -f v4l2 -video_size 640x480 -i /dev/video0 -f alsa -i default -c:v libx264 -preset ultrafast -c:a aac webcam.mp4
ffmpeg -f v4l2 -video_size 1100x1100 -i /dev/video0 -f alsa -i default -c:v libx264 -preset ultrafast -c:a aac webcam2.mp4


##### ffmpeg Image output:
###### -r: framerate of output
ffmpeg -i inputfile.mp4 -r 1 -f image2 image-%3d.jpeg # one per second
ffmpeg -i inputfile.mp4 -frames:v 1 thumb.png # one

#### ffmpeg GIF output (scaled)
ffmpeg -i D-fin.mp4 -vf palettegen D-fin.palette.png
ffmpeg -i D-fin.mp4 -i D-fin.palette.png -filter_complex '[0]scale=320:-1:flags=lanczos[x];[x][1]paletteuse' D-fin.gif

### ffmpeg Stream webcam video to a remote ffmpeg target.
ffmpeg -f v4l2 -video_size 640x480 -pixel_format yuyv422 -i /dev/video0 -c:v libx264 -crf 28 -preset ultrafast -f flv tcp://0.0.0.0:4434/?listen


### ffmpeg cam audio and screen sharing

ffmpeg \
    -f x11grab -video_size 1366x768 -framerate 25 -i :0.0 \
    -f v4l2 -video_size 200x200 -framerate 25 -i /dev/video0 \
    -filter_complex "[0][1]overlay=x=W-w:y=H-h" \
    -f pulse -ac 2 -i default -vcodec libx264 test.mkv

### ffmpeg subtitles
#### fmmpeg subtitles Use the libass library make sure your ffmpeg install has the library in the configuration --enable-libass
#### ffmpeg subtitles 1 - First convert the subtitles to .ass format:
ffmpeg -i sub.srt sub.ass
#### ffmpeg subtitles 2 - add them to a video filter
ffmpeg -i in.mp4 -vf ass=sub.ass out.mp4

### ffmpeg extract all frames of video
ffmpeg -i input.mp4 thumb%04d.jpg -hide_banner

### ffmpeg frame each seconds
ffmpeg -i input.mp4 -vf fps=1 thumb%04d.jpg -hide_banner

### ffmpeg rotate a video
ffmpeg -i in.mov -vf "transpose=1" out.mov

0 = 90CounterCLockwise and Vertical Flip (default)
1 = 90Clockwise
2 = 90CounterClockwise
3 = 90Clockwise and Vertical Flip

### ffmpeg trimming
ffmpeg -ss [start] -i in.mp4 -t [duration] -c copy out.mp4

-ss specifies the start time, e.g. 00:01:23.000 or 83 (in seconds)
-t specifies the duration of the clip (same format).
Recent ffmpeg also has a flag to supply the end time with -to.
-c copy copies the first video, audio, and subtitle bitstream from the input to the output file without re-encoding them. This won't harm the quality and make the command run within seconds.

### ffmpeg Slow a video using a filter. This example slows the video by four times.
ffmpeg -i in.mp4 -filter:v "setpts=4.0*PTS" out.mp4

### ffmpeg crop video Crop a 80x60 square at position (200, 100).
ffmpeg -i in.mp4 -filter:v "crop=80:60:200:100" -c:a copy out.mp4