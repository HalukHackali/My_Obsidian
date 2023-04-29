#linux 

```bash
ffmpeg -i input.mp4 -c:v dnxhd -profile:v dnxhr_hq -pix_fmt yuv422p -c:a pcm_s16le -f mov output.mov 
```

```bash
ffmpeg -i input.mp4 -c:v dnxhd -profile:v dnxhr_hq -pix_fmt yuv422p -c:a pcm_s16le -f mov output.mov 
```

```bash
ffmpeg -i 5.mp4 -c:v prores_ks -profile:v 3 -qscale:v 9 -c:a pcm_s16le 5.mov 
```

```bash
fmpeg -i input.mp4 -c:v cfhd -c:a pcm_s32le output.mov 
```