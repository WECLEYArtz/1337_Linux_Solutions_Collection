# 1337_Linux_Solutions_Collection
A collection to solve comon linux difficulty for 1337 posts (sepecially E3)
Or list for unsolved known ones


## Sound issue [SLOVED]
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


## Laggy Brave browser [SLOVED]

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


## Mac keyboard layout [SLOVED]

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


# UNSOLVED
uuuuuuh, everything?
