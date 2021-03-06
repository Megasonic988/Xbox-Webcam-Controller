CCWJ Helmet Camera Controller
By Kevin Wang and Goetz Dapp

Description
This Python script allows you to control the parameters of a connected webcam
(e.g. pan, exposure, zoom) using an XBOX controller. Written for running
on OpenSuse Leap 42.2 with a Logitech webcam.

Dependencies:
- Python 3
- xboxdrv (driver for XBOX controller)
- v4l2-utils (driver for webcam)
- guvcview (for viewing the webcam output)
- ffmpeg (for adding the logo watermark)
- pygame (for interfacing XBOX controller and Python. Install with pip)
- wmctrl (for window management)

To run:
1. Make sure xboxdrv is running ('sudo xboxdrv'). For ease, run on system startup.
2. Run script with './launch.sh' from terminal

Extra Tips:
- to view all the controls available for the webcam and their setting ranges,
run 'v4l2-ctl -l'
- to run guvcview with or without a GUI, set --gui=<none/gtk3>, respectively, in
controller.py
- to bring a guvcview window to the front, run:
'wmctrl -ir "Guvcview" -b add,maximized_vert,maximized_horz'
- sending SIGUSR1 to guvcview starts/stops recording ('killall -SIGUSR1 guvcview')
- to record with ffmpeg:
'ffmpeg -f video4linux2 -r 25 -i ' + video + ' -f alsa -i ' + audio + '
-acodec aac -vcodec mpeg4 -y vid.mp4' (where video and audio are the devices)
- to add watermark to video:
'ffmpeg -i Output/' + filename + '.mkv -i logo.png -filter_complex
"overlay=10:10" Output/ ' + filename + '.mkv')

Code Description:
- init.py: starts tkinter GUI and runs the controller loop
- controller.py: parses XBOX controller inputs, sets webcam settings accordingly
