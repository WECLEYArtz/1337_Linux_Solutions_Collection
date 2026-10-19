# 1337_Linux_Solutions_Collection
A collection to solve comon linux difficulty for 1337 posts (sepecially E3)
Or list for unsolved known ones


## Sound issue
Create the following directory
`mkdir -p ~/.config/systemd/user`

Open this file with your editor
`~/.config/systemd/user/restart-pulseaudio.service`

Insert the following content:
```
[Unit]
Description=Restart PulseAudio after login

[Service]
Type=oneshot
ExecStart=/usr/bin/systemctl --user restart pulseaudio

[Install]
WantedBy=default.target

systemctl --user daemon-reload                        
systemctl --user enable restart-pulseaudio.service
```


## Laggy Brave browser

- Create the file:
```
~/.var/app/com.brave.Browser/config/BraveSoftware/Brave-Browser/brave-flags.conf
```

- Insert The Content:
```
--enable-features=AcceleratedVideoDecodeLinuxZeroCopyGL
```
or
```
--enable-features=AcceleratedVideoDecodeLinuxZeroCopyGL,AcceleratedVideoDecodeLinuxGL,AcceleratedVideoEncoder
```

- Save, Then restart brave

should work with chromium too, check the link > [source](https://universal-blue.discourse.group/t/launch-chromium-browser-with-flags-flatpak/8358)

## Laggy Youtube
Just disable Ambient mode
Open a youtube video > click the gear icon > disable Ambient mode

## Mac keyboard layout

if you want to mimic the old "Cherry Strait 3.0",
you just need to swap `alt` and `super`:

```
setxkbmap -option altwin:swap_alt_win
```

or make a startup script to automaticall detect it the keyboard and swap
```sh
if lsusb | grep -q "CHERRY Wired Keyboard"; then
    setxkbmap -option altwin:swap_alt_win
fi
```

NOTE: to unset the change:
`setxkbmap -option`


## Failed playback
You may encounter this error message:
"If playback doesn't begin shortly, try restarting your device" in youtube.
this could be due to a pulseaudio configuration causing it to shutdown when left unused/idle

you can try this small solution, worked for me
copy the default `default.pa` to  your user config:
```
cp /etc/pulse/default.pa ~/.config/pulse/default.pa
```
comment the line 
```
load-module module-suspend-on-idle
```

restart and enjoy listening to whatever.

To only re-activate the audio, just do
```systemctl --user restart pulseaudio.service```

[Solution Source](https://www.reddit.com/r/pop_os/comments/n82egy/pulseaudio_failed_to_create_sink_input_sink_is/) 
