### ffplay

#### ffplay open cam
ffplay /dev/video0

#### ffplay open cam good res no lag
ffplay -f v4l2 -input_format mjpeg -video_size 1920x1080 -framerate 60 -i /dev/video0 