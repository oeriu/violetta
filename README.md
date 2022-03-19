## violetta
this repository was made to prevent users from ever breaking their keyboards

### lists of available walkthroughs
(c)[chroot](#chroot) (w)[Wayland](#wayland) 

## chroot
my essay's deadline is in 30 minutes, please help me!

1. download live image at https://voidlinux.org/download/
2. flash the iso to usb stick using Rufus or `dd`
3. change Boot Order to usb stick
4. (optional) If issues are happening, edit boot options

    black screen? add `nomodeset` to boot options

5. enter login credentials 
   ```
   login: anon
   passw: voidlinux
6. ```
   mount -t auto /dev/sda# /dev/void
   chroot /mnt/void
   ```
7. check if xbps is working `xbps-install -Su`
8. do anything to fix your system

## Wayland
xorg is throttling my cpu, how do i install no-wayland?
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
6. do commands
```
mkdir -p /tmp/swaytmp
export XDG_RUNTIME_DIR=/tmp/swaytmp
```  
7. in your current tty; do `exec sway`
