# GIF-O-MATIC-Video-Tool

I'd like to present my latest tool, the GIF-O-MATIC!

- "get the look of .GIF, without the hassle!"

\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\WHY?!\\\\\\\\\\\\\\\\\\\\\\\\

Okay I admit it, I love 90's web design aesthetics... I grew up with dial up modems, limited hard drive and internet, and playing video games with shitty textures, for a PC with 128mb of VRAM to display them on.
There's a certain beauty to me about the limitations of the hardware unwittingly making a whole new aesthetic. The dither noise, low resolution and limited colour space all become a sort of canvas for the modern day painter.
Now looking back (on a 4k 180hz HDR monitor, nursing a dram of whiskey) I feel a charm and nostalgia for those gritty, simpler graphics. in many ways, the texture of a .GIF is to Millenials what tape hiss and vinyl crackle is to Gen X'ers 
it scratches the same part of my brain that enjoys 12bit/22.50khz audio files, I shouldn't like something so inherently inferior, but I do!
anyway, long story short- enjoy GIF-O-MATIC!

\\\\\\\\\\\\\\\\\\\\\\\\\\\\HOW TO USE:\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\

Take a video file of your choice, drag and drop it onto one of the .BAT files.
"GIF-O-MATIC FRAMES.bat" Video file will automatically be converted into a stream of frames in .PNG format at source framerate and 800px width, a new folder will be created in the original files address with the frames inside.
"GIF-O-MATIC CLIP.bat" Video file will be automatically converted into a .AVI video file, and placed in the source files address. Settings for input / output resolution and frame rate can be found by editing the .bat file.

- "Sign me up!"

\\\\\\\\\\\\\\\\\\\\\\\IF YOU GET AN ERROR:\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\

When you type ffmpeg in a command window, Windows looks for ffmpeg.exe in a list of folders called the PATH. If ffmpeg isn’t in one of them, you get “‘ffmpeg’ is not recognized as an internal or external command”, and the .bat stops. Having ffmpeg downloaded isn’t enough on its own.

Easiest way to set it up (Windows 10/11)

Open Command Prompt or PowerShell.
Run winget install Gyan.FFmpeg. This installs it and adds it to the PATH.
Close and reopen the window, then run ffmpeg -version. If you see a version number, it’s ready.

If winget isn’t available

Download a Windows build of ffmpeg from ffmpeg.org’s download page (the “essentials” build from gyan.dev is fine) and unzip it to something like C:\ffmpeg.
Search Windows for “Edit the system environment variables”, open Environment Variables, select Path under your user variables, and choose Edit.
Add C:\ffmpeg\bin (the folder containing ffmpeg.exe and ffprobe.exe).
Open a new command window and run ffmpeg -version to check.

Skipping the PATH
You could instead copy ffmpeg.exe and ffprobe.exe into the same folder as gif_look.bat and palette_252.png. That should work when you drag a file onto the .bat, but I haven’t tested it, so the PATH route is the reliable one.

Once ffmpeg -version works, drag a clip onto the .bat of choice, and wait. 

\\\\\\\\\\\\\\\\\\\\\\\\\\\\\NOTES:\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\
I think you'll be happy not only with the resulting look, but with the speed and efficiency of this process.
A word of warning, A short video around 100mb, can easily become a 650+mb file at source resolution/fps, so consult the edit page if you want less extreme file sizes.
I find using "native" output resolution with a width of 480px and a frame rate of 15 yields a crunchy authentic looking image that could pass for a .GIF
but is also very efficient in file size. my test video went from 91 to 35 megabytes after conversion.

\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\GIF-O-MATIC FRAMES.BAT Default Settings\\\\\\\\\\\\\\\\\\
rem ---------------- SETTINGS (edit these) ----------------
rem  Effective GIF resolution (pixel width). Pick a number that divides
rem  your video width evenly for clean square pixels, e.g. 960 for 1920,
rem  640 for 1920, 480 for 1920.
set WIDTH=480
rem  Dither: floyd_steinberg | burkes | sierra2 | sierra2_4a | heckbert | atkinson | bayer | none
set DITHER=floyd_steinberg
rem  Frame rate. Leave empty to keep the original, or e.g. 12 or 15 for a GIF-like frame rate.
set FPS=
rem  How the picture is shrunk before dithering: bicubic (soft) | neighbor (harsh) | area
set DOWNSCALE=bicubic
rem --------------------------------------------------------

\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\GIF-O-MATIC CLIP.bat Default Settings\\\\\\\\\\\\\\\\\\\\\\
rem ---------------- SETTINGS (edit these) ----------------

rem  WIDTH = the effective GIF resolution (pixel width of the dither grid).
rem  Smaller = chunkier pixels.  e.g. 320, 480, 640, 800
set WIDTH=480

rem  OUT_WIDTH = pixel width of the finished file.
rem    0       same size as your original video
rem    auto    closest clean multiple of WIDTH to the original size (square, even pixels)
rem    native  same as WIDTH (small file, scale it up in your editor with no smoothing)
rem    1280    or any number you like
set OUT_WIDTH=native

rem  FPS = output frame rate. Leave empty to keep the original.
rem  GIF-like speeds: 10, 12, 15
set FPS=15

rem  FORMAT = avi | mp4 | png
rem    avi  lossless, keeps every dither pixel exact (big files)
rem    mp4  small and plays anywhere, but lossy: dither colours drift a little
rem    png  lossless image sequence in a folder
set FORMAT=avi

rem  AVI_CODEC = utvideo | rawvideo   (only used when FORMAT=avi)
rem    utvideo   lossless and much smaller. Plays in VLC / mpv; editors
rem              such as Premiere and Resolve need the Ut Video codec installed.
rem    rawvideo  uncompressed. Opens almost everywhere but files are huge.
set AVI_CODEC=utvideo

rem  Dither: floyd_steinberg | burkes | sierra2 | sierra2_4a | sierra3 | heckbert | atkinson | bayer | none
set DITHER=floyd_steinberg

rem  DOWNSCALE = how the picture is shrunk before dithering: bicubic (soft) | neighbor (harsh) | area
set DOWNSCALE=bicubic

rem --------------------------------------------------------


\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\REFERENCES:\\\\\\\\\\\\\\\\\\
https://pixelsynth.art/algorithms/floyd-steinberg
https://www.gyan.dev/ffmpeg/builds/
Thanks to Claude AI for helping me build the tool
