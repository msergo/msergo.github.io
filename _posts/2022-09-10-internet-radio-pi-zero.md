---
layout: post
title:  "Tiny project: web radio on Raspberry Pi Zero W and Bluetooth speaker"
---

II have an excellent [Raspberry Pi Zero W](https://www.raspberrypi.com/products/raspberry-pi-zero-w/) at my home, and for a long time, it served just one purpose: hosting a local DNS server with Adblock functionality created with [`Pi-hole`](https://pi-hole.net/).


The board works surprisingly well and is stable, it almost had no hangs or unexpected behavior, same as no maintenance was required. The only thing one should care about is a decent 5V power supply. I use a 5W one from some old office phone.

Although Pi Zero is tiny, I realized that it still has free resources for more than just a DNS. As a nice bonus, it also has a Bluetooth interface with audio capability, so I came up with the idea to use it as a home web radio player available from the local network and connected to a speaker wirelessly. I wanted a service that works as a background music player without a need to connect my active devices like my phone or laptop to the speaker. 

It was supposed to live only in the local network, so the design should be minimalistic. No things like automatic deployments or authorizations are considered, just buttons to play and stop music :)


![Minimalistic page](/assets/images/pi-radio-screen.jpg){: width="300"}

#### Programming part
A Python web app based on the [`Bottle`](https://bottlepy.org/docs/dev/) framework. After the user clicks in a browser the station to listen, the app spawns a music player in the background using Python's `subprocess.Popen`, and its audio output is streamed to the speaker. 

Initially, the `mplayer` has been chosen as playing util, but later I switched to headless vlc -- `cvlc`. Both work pretty nicely.


#### Setup of Bluetooth speaker
My Raspberry piece runs on Raspbias distro without GUI, so all the config should be done using SSH. But it turned out to be not as tricky as I initially expected.

Find and pair your speaker

```bash
$ bluetoothctl scan on
Discovery started
[CHG] Controller 22:11:F9:18:8C:C8 Discovering: yes
[NEW] Device D8:9C:67:B4:33:18 SOME_OTHER_DEVICE
[NEW] Device B8:08:EB:7A:AC:C3 SPEAKER_HERE
# pair the SPEAKER_HERE device
bluetoothctl pair "B8:08:EB:7A:AC:C3"
bluetoothctl trust "B8:08:EB:7A:AC:C3"

```

Install PulseAudio Bluetooth profile loader

```bash
$ sudo apt install pulseaudio-module-bluetooth
# add pi user to bluetooth group
$ sudo usermod -a -G bluetooth pi
```
Install [bluez-alsa](https://github.com/Arkq/bluez-alsa)
```bash
$ sudo apt-get install bluealsa
$ vi ~/.asoundrc
# add the default config
defaults.bluealsa.service "org.bluealsa"
defaults.bluealsa.device "XX:XX:XX:XX:XX:XX" # MAC of the speaker
defaults.bluealsa.profile "a2dp"
defaults.bluealsa.delay 10000 
```

Verify that it works
```bash
$ sudo apt install mplayer
$ mplayer -softvol -vo null -ao alsa:device=bluealsa file_example.wav 
```

Now it's time to start the app
```bash
$ cd mplayer-pi
$ virtualenv -p /usr/bin/python3 env
$ . env/bin/activate
$ pip install -r requirements.txt
$ python main.py 
```

After a successful start, it’s possible to navigate to the page in the browser and run play some music. The source code of the example application can be found on [Github](https://github.com/msergo/mplayer-pi)

#### Conclusion
Radio app lives in my network for quite a long time already.
Raspberry Pi is a great thingy for tinkering with, and after running there 2 applications for 24/7 it still has some resources. Also, I don't use any radiators or coolers on it.
```bash
$ free -h
              total        used        free      shared  buff/cache   available
Mem:          430Mi        79Mi        58Mi        10Mi       292Mi       286Mi
Swap:          99Mi       1.0Mi        98Mi
```

Happy coding!