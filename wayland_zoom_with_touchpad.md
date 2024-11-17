1) Install `libinput-gestures` and set like this:

<pre>
$ libinput-gestures -l
/usr/bin/libinput-gestures:694: DeprecationWarning: distutils Version classes are deprecated. Use packaging.version instead.
  if Version(libvers) >= Version('1.8'):
libinput-gestures: session gnome+wayland on Linux-6.11.5-200.fc40.x86_64-x86_64-with-glibc2.39, python 3.12.7, libinput 1.26.2
Hash: bda1394ca92ca61efd2e26a93f9e7f24
Gestures configured in ~/.config/libinput-gestures.conf:
swipe up           _internal ws_up
swipe down         _internal ws_down
swipe left         xdotool key alt+Right
swipe right        xdotool key alt+Left
pinch in           xdotool key super+s
pinch out          xdotool key super+s
<b>pinch in         2 xdotool key ctrl+minus</b>
<b>pinch out        2 xdotool key ctrl+plus</b>
libinput-gestures: device /dev/input/by-path/pci-0000:00:15.1-platform-i2c_designware.1-event-mouse(event7): DLL07BE:01 06CB:7A13 Touchpad
libinput-gestures is installed.
libinput-gestures is set up as a desktop application.
libinput-gestures is currently running as a desktop application.
libinput-gestures is set to autostart as a desktop application.
libinput-gestures is using custom configuration file.

</pre>

2) Set `chrome://flags/#ozone-platform-hint` to `Auto`

3) If `Remote desktop`:`Allow remote interaction` popup appeared while pinching, then run `sudo rpm --nodeps -e xdg-desktop-portal-gnome` to avoid it.
