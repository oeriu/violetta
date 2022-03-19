## violetta
this repository was made to prevent users from ever breaking their keyboards

### lists of available walkthroughs
(c)[chroot](#chroot) (w)[wayland](#wayland) 

## chroot
my essay's deadline is in 30 minutes, please help me!

1. download live image at https://voidlinux.org/download/
2. flash .iso file to usb stick using Rufus or `dd`
3. reboot and change boot order to usb stick
4. (optional) If issues are happening, configure boot options

    black screen? add `nomodeset` to boot options

5. enter login credentials 
   ```
   login: anon
   passw: voidlinux
6. find where linux is installed `lsblk`

7. ```
   mkdir /mnt/void
   mount -t auto /dev/sda# /mnt/void
   chroot /mnt/void
   ```
8. check if xbps is working `xbps-install -Su`
9. do anything to fix your system

## wayland
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
6. set XDG_RUNTIME_DIR
```
mkdir -p /tmp/swaytmp
export XDG_RUNTIME_DIR=/tmp/swaytmp
```  
7. in current tty; do `exec sway`
