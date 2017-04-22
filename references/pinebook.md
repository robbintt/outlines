### Suspend

Two methods... you have to adjust the brightness afterwards

1. Press `Fn-Esc`
2. Type `$ systemctl suspend`

### Adjusting brightness

# stack overflow says any value 0 to 20 works, but it was at 255 after suspend
#sudo su -c 'echo 255 > /sys/class/backlight/lcd0/brightness'
sudo su -c 'echo 0 > /sys/class/backlight/lcd0/brightness'
