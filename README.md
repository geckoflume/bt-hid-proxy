# bt-hid-proxy
Idea is to allow a bluetooth keyboard to communicate with a device that can't support native bluetooth due to hardware or software limitations.

The simple magic trick is to use a raspberry pi (4 or Zero) in gadget mode, meaninng it's physically plugged into the device via USB to do the keyboard emulation after getting instructions from the bluetooth keyboard thanks to `evdev`.

## Instructions
- Setup your pi with raspberry pi OS (network, ssh, accounts...)
- Pair your keyboard to the pi
    ```bash
    bluetoothctl
    > scan on
    > pair <keyboard MAC>
    > trust <keyboard MAC>
    > connect <keyboard MAC>
    > quit
    ```
- Ensure `/dev/input/event1` is your keyboard input device with `cat /proc/bus/input/devices`, otherwise replace device path in [app/main.py](app/main.py#L9)
- Run `sudo ./setup.sh`
- (Optional) Turn your pi to read-only to save your microsd card
    ```bash
    sudo raspi-config
    > 4 Performance Options
    > P3 Overlay File System
    ```
- Shutdown your pi (`sudo shutdown -h now`)
- (Optional) In case you're using a raspberry pi zero, connect the usb OTG port to your computer and disconnect the usb power 
- Enjoy your new "wired" keyboard

## Credit
Some helpful stuff I used for reference
- https://mtlynch.io/key-mime-pi/
- https://gitlab.com/dcro/quimby/-/blob/master/quimby-relay
- https://github.com/gvalkov/python-evdev
- https://github.com/mikerr/pihidproxy
- https://forums.raspberrypi.com/viewtopic.php?t=138578