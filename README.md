# Analog-TV-Antenna-Rasberry-Pi
Create a analog tv Antenna with rasberry pi

## Requirements
* Rasberry Pi with Composite Video output (https://www.raspberrypi.com/documentation/computers/config_txt.html#composite-video-mode)
* Converter from composite video to antenna/coax (i used an old Videocassette recorder with composite video in and antenna out)
* Amplifier for cable radio (87 to 860 MHz, you need only the broadcast channels for tv)
* Own build coax antenna, looks like a T or ´´´__in__.__out__´´´, in and out cables in different directions
* ubuntu server or something similiar
* mplayer, vlc doesnt work remotly

## Set-up
Prepare the Rasberry pi with the right video output, you may try different settings in the ´config.txt´ (https://www.raspberrypi.com/documentation/computers/config_txt.html#composite-video-mode) like ´sdtv_mode´ or enable_tvout´.
I was sucessfull with this configuration:
´´´sdtv_mode=2
sdtv_aspect=1
disable_overscan=1
sdtv_disable_colourburst=0
enable_tvout=1´´´

Then connect the rasberry with the right cable (the cinch cable with audio and video signals is not the cheap one, but the one you can use also for apple products) to the video decoder or videocasette recorder. Ampliefie the signal and connect you antenna, voila, you build your own digital analog tv antenna signal device.

## Code for Videos
Code examples to play videos or even a webcam on the rasberry pi remotly over ssh: 
```
#start mplayer
mplayer -zoom -xy 720 Videos/video.mp4 -fs
mplayer -loop 0 -zoom -xy 720 -fs  Videos/
mplayer -zoom -xy 720 -playlist playlist.txt -fs

#start mplayer in the background
ssh -n -f ubuntu@ip "sh -c 'mplayer -zoom -xy 720 Videos/video.mp4 -fs > /dev/null 2>&1 &'"

#kill mplayer
pkill mplayer

#show terminal output
echo "hi " > /dev/tty1
screenfetch > /dev/tty1

#start webcame output with different options
mplayer  tv:// -tv driver=v4l2:device=/dev/video0:width=854:height=480:fps=30:outfmt=yuy2:saturation=30:hue=-100:brightness=-30 
spacebar: stop/play, 
1-2= contrast
3-4= brightness!

5-6= colour
7-8=saturation
```

## Pictures:!
![party](https://user-images.githubusercontent.com/55106217/194853478-f946755a-989e-4667-909f-31b6f6c1705f.jpeg)

![test](https://user-images.githubusercontent.com/55106217/194853364-847bece8-7800-48d1-a089-7cab929d4a81.jpeg)

## Credits and more informations
* https://github.com/ssshake/pi-uhf-tv-station
* https://www.reddit.com/r/raspberry_pi/comments/phgj4f/made_a_wireless_raspberry_pi_based_crt_tv_tester/
* https://spectrum.ieee.org/hack-an-analog-tv-into-a-geek-tv
