# Pi Sensor Monitor
## Intro

This project is intended for use with hydroponic gardens to monitor the humidity and temperature.

This is designed for use with the humiture sensor and I2C LCD screen from the [SunFounder Sensor](https://www.sunfounder.com/products/sensor-kit-v2-for-raspberrypi?_pos=1&_sid=d7c8153f8&_ss=r) kit.

## Pi Breadboard Setup
Connect the [humiture sensor](https://docs.sunfounder.com/projects/sensorkit-v2-pi/en/latest/lesson_28.html) and [LCD screen](https://docs.sunfounder.com/projects/sensorkit-v2-pi/en/latest/lesson_30.html) components

## Setting up to run on pi launch
To use the LCD screen component, you'll need to [enable I2C](https://docs.sunfounder.com/projects/sensorkit-v2-pi/en/latest/appendix/i2c_configuration.html) on the raspberry pi.

Then, clone this repo. You could run `sudo python 00_humitor_to_screen.py` to start the script that makes the sensor work. Alternatively, we could configure the script to run when the pi starts so that we don't need to run with any additional peripherals attached.

First, if you've cloned into a parent folder other than `/home/pi`, update line 1 of [launcher.sh](./launcher.sh) to match where the repo/script is located.

Then, make the launcher script executable by running this shell command:
```
chmod 755 launcher.sh
```

We can use cron to run the launcher script at startup:

```
sudo crontab -e
```
brings up the crontab configuration. 

You can then add

```
@reboot sh /home/pi/bbt/launcher.sh >[path_to_logfile] 2>&1
``` 

to the end of this file run this script at startup.

See [instructables guide](https://www.instructables.com/Raspberry-Pi-Launch-Python-script-on-startup/) for a more in-depth guide to launching on startup from cron.