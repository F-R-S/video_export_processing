# Video Export for Processing

This library interfaces with ffmpeg and makes it easy to export video files out
of Processing.

## Example

```java
import com.hamoid.*;

VideoExport videoExport;

void setup() {
  size(600, 600);
  videoExport = new VideoExport(this, "hello.mp4");
  videoExport.startMovie();
}
void draw() {
  background(#224488);
  rect(frameCount * frameCount % width, 0, 40, height);
  videoExport.saveFrame();
}
void keyPressed() {
  if (key == 'q') {
    videoExport.endMovie();
    exit();
  }
}
```

## ffmpeg

You need to download and install [ffmpeg](http://ffmpeg.org/) on your system before you can use this library.
Note that you might already have it installed! You can find out by typing ffmpeg or ffmpeg.exe
in the terminal. If the program is not found:

* GNU/Linux systems: use your favorite package manager.
* Windows: get a [static 32bit or 64bit binary](http://ffmpeg.zeranoe.com/builds/)
* Mac: get a [static 64bit binary](http://evermeet.cx/ffmpeg/)

For more details and download links, check the official ffmpeg website: [http://ffmpeg.org](http://ffmpeg.org/)

When you start a Processing sketch that uses this library you may be asked to indicate the location
of your ffmpeg executable. This may happen once per sketch.

## faq

### I changed the location of ffmpeg and the library stopped working. What can I do?

Add ``` videoExport.forgetFfmpegPath()``` to your setup(), run your program once, then remove that line. This will trigger the library asking for the location of ffmpeg again, so you can point to the new location of ffmpeg.

### Sometimes the resulting mp4 video files are not working. Why?

mp4 files contain essential metadata at the end of the file.
The video export library saves this metadata when you call the
```endMovie()``` method. If you don't call it, the movie may be
incomplete. The endMovie() method was added on version 0.1.5.

### I see an ffmpeg error related to "crf". Why?

This happens if your copy of ffmpeg does not include the h264 encoder.
Not all ffmpeg binaries are equal, some include more features than others.
Try downloading a different or more recent binary. Let me know if that
doesn't work.

## change log

* 0.1.5 - December 2nd, 2016
  * Refactoring. Clean up code.
  * Add .startMovie() and .endMovie() to prevent possible "missing-end-of-movie corruption".
  * Allow attaching a sound file to the produced movie.
  * Allow exporting multiple video files using the same videoExport object.
* 0.1.4 - August 4th, 2016
  * Attempt to fix randomly corrupted videos on Windows 
* 0.1.3 - July 24th, 2016
  * Add webcam saving example.
  * Add getFfmpegPath() public method (requested by [@ffd8](https://github.com/ffd8)).
  * Replace PGraphics with PImage, enables webcam/movie saving (requested by [@transfluxus](https://github.com/transfluxus)).
* 0.1.1 - June 15th, 2016
  * Use .waitFor() to reduce chances of video corruption.
* ...
* 0.0.1 - January 25th, 2015

## Download

http://funprogramming.org/VideoExport-for-Processing/
