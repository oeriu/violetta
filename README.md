## void-frustation
this repository was made to prevent users from ever breaking their keyboards

### lists of available walkthroughs
(c)[chroot](#chroot) (w)[Wayland](#wayland) 

## chroot
made when I did something stupid

1. Download live image at https://voidlinux.org/download/
2. Flash the iso to usb stick using Rufus or `dd`
3. Change Boot Order to usb stick
4. (OPTIONAL) If issues are happening, edit boot options

    black screen? add `nomodeset` to boot options

5. Enter credentials 
   ```
   login: anon
   passw: voidlinux
   ```
6. mount -t auto /dev/sda# /dev/void </br>
   chroot /mnt/void </br>
   
7. Check if repos and xbps commands are working `xbps-install -Su`

## Wayland
this is when I couldn't get enough of ripping all my hair out
### Installing Wayland Compositors
#### Sway with seatd 

1. sudo xbps-install `mesa-dri` `seatd` `sway`
- mesa-dri - graphics driver
- seatd  - minimal seat management daemon
- sway - wayland compositor
2. sudo ln -s /etc/sv/seatd /var/service
3. sudo usermod -aG _seatd your_user
4. cp /etc/sway/config ~/.config/sway/
5. sudo chmod +x /usr/bin/sway (solves the common issue where first time wayland users encounter bad luck)

```
[wlr] [libseat] [libseat/backend/logind.c:310] Could not activate session: Permission denied [wlr]
[libseat] [libseat/libseat.c:79] No backend was able to open a seat [wlr] 
[backend/session/session.c:84] Unable to create seat: Function not implemented [wlr] 
[backend/session/session.c:218] Failed to load session backend 
[sway/server.c:53] Unable to create backend
```

6. do this commands
```
mkdir -p /tmp/swaytmp
export XDG_RUNTIME_DIR=/tmp/swaytmp
```
7. goto your tty </br>
  you can cycle ttys from 1 - # </br>by doing ctrl + alt + F(number) / F1 / F2 / F3
  
8. in your current tty; do `exec sway`
