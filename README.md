# FPS Conform

:warning: Works for me but not tested much! I've used this on Arch Linux with files that have stereo and 5.1 audio.

Bash script to conform between NTSC and PAL.

## What's conforming?

Conforming is either speeding up or slowing down the duration to match the desired output framerate. This is generally how films and TV shows are converted between standards.

The alternative is repeating or dropping frames to change the frame rate, and that's bad.

## Any change in quality?

### Video

No. For the video this is done losslessly without re-encoding. The duration will be longer moving from PAL to NTSC and vice-versa.

### Audio

Yes. For the audio it is changing the tempo. This means the pitch is adjusted accordingly to match the new speed. In other words, there should be little perceptible difference in pitch between the original and the conformed one. This is a lossy process.

The audio is re-encoded with AC3 at 48000Hz/320K.

## Requirements

### Not Included

#### mkvmerge

Part of the [`mkvtoolnix`](https://www.bunkus.org/videotools/mkvtoolnix/) package usually. Used to change the video framerate.

#### ffmpeg and ffprobe

Both usually come with [`ffmpeg`](https://www.ffmpeg.org/). Uses `ffprobe` to get the framerate of the input file and `ffmpeg` to convert the audio while maintaining pitch.

### Included

#### srtshift

Part of [`mplayer-tools`](http://mplayer-tools.sourceforge.net/). I couldn't even find a package for this in Arch! So since it's a simple Perl script it's just included. Used to convert the frame rate for SRT subtitles.

## Running

Provide the folder where your MKV videos to be converted are followed by the framerate to conform to. Valid framerates are 23.976, 24, and 25.

It *should* not overwrite your originals, however it may be safest to _make a backup copy_!

The first embedded subtitle will be used, otherwise if there's an SRT subtitle of the same name next to the video file it will use that.

```
bash fps_conform.sh [folder] [framerate]
```

This will output the finished files in a `converted` folder in the same directory as the script.
