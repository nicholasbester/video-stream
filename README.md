## Commands to test

### Step 1 - FFMPEG is serving a looping video
```
ffmpeg -re -stream_loop -1 -i videoloop.mp4 -c:v libx264 -preset veryfast -maxrate 3000k -bufsize 6000k -vf "scale=1280:720" -g 50 -c:a aac -b:a 128k -f hls -hls_time 2 -hls_list_size 3 -hls_flags delete_segments -start_number 1 public/media/live/stream.m3u8
```

### Step 2 - Start the Express Server
```
node server.js
```

### Step 3 - Open the browser and go to the following URL
```
http://localhost:3000
```

## Commands to run from SMP 111

### Step 1 - Set Up SMP 111 to Stream via RTMP:
Ensure that the SMP 111 is configured to stream using the RTMP protocol. The RTMP stream URL will typically look something like this: rtmp://<SMP_111_IP>/live/stream.

### Step 2 - Run FFmpeg to Convert RTMP to HLS:
ffmpeg -i rtmp://<SMP_111_IP>/live/stream -c:v libx264 -preset veryfast -maxrate 3000k -bufsize 6000k -vf "scale=1280:720" -g 50 -c:a aac -b:a 128k -f hls -hls_time 2 -hls_list_size 3 -hls_flags delete_segments -start_number 1 public/media/live/stream.m3u8

Change "SMP_111_IP" to the SMP 111's IP address.

### Step 3 - Start the Express Server
```
node server.js
```

### Step 4 - Open the browser and go to the following URL
```
http://localhost:3000
```