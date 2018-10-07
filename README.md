mqtt-to-gatt-server
===================

*Still under dev.* Stream data from a MQTT server (which might be from a remote BLE device) to local Bluetooth LE services' characteristics.

Further below is the original README from Jumper Labs - full credit to them for sharing their great project that really helps reduce much time/effort trying to resolve issues in the undocumented bluez examples (test folder).

Right now, I am currently using Bluez 5.50 with good success so far and no need to enable 'experimental' features. For testing, I recommend and really want to thank Nordic semi for providing their great free Android app named 'nRF Connect'.

Header format of most added files are from: http://web.archive.org/web/20111010053227/http://jaynes.colorado.edu/PythonGuidelines.html#module_formatting (linked from https://stackoverflow.com/questions/1523427/what-is-the-common-header-format-of-python-files).

---

LICENSE
-------

mqtt-to-gatt-server 1.0 Copyright (C) 2018 Kasidit Yusuf.

Released under the GNU GPL v2 License - see COPYING file (from BlueZ project) for details. This project is a fork of 'python-gatt-server' (https://github.com/Jumperr-labs/python-gatt-server.git) originally by Jumper Labs which is based on 'BlueZ' (http://www.bluez.org/) example code. Credit goes to respective authors and see copyright notices of respective projects for further details.

---

Forked project's original README
--------------------------------

# Python BLE GATT Server (peripheral)
GATT is constructed out of one or more server devices (BLE peripherals) and a client device (BLE central).

A GATT server is usually a small device such as a sensor, but for some use cases you might want to have a Linux computer such as a RPi used as a GATT server. This example is meant to demonstrate how this can be done.


## Setup
The instructions in this document were tested on Ubuntu 16.04.

### Bluez Installation
On most distributions, you will need to upgrade Bluez in order to make this work.

Install dependencies:
```bash
sudo apt-get update
sudo apt-get install libudev-dev libical-dev libreadline-dev libglib2.0-dev libdbus-1-dev
```

Download and install Bluez

```bash
wget http://www.kernel.org/pub/linux/bluetooth/bluez-5.45.tar.xz
tar xvf bluez-5.45.tar.xz
cd bluez-5.45/
./configure
make
sudo make install
```

Enable experimental features for the bluetooth driver: 
- `sudo nano /lib/systemd/system/bluetooth.service`
- Add `--experimental` to `ExecStart`. The line should look like this: 

    `ExecStart=/usr/local/libexec/bluetooth/bluetoothd --experimental`

Reload the service:
```bash
systemctl daemon-reload
sudo service bluetooth restart
```

### virtualenv
Install dependencies: `sudo apt-get install virtualenv python-dev libdbus-1-dev libdbus-glib-1-dev python-gi`

`cd` to the the root of this repository and:

```bash
virtualenv venv
source venv/bin/activate
pip install -r requirements.txt
ln -s /usr/lib/python2.7/dist-packages/gi venv/lib/python2.7/site-packages/
```

## Usage
Start the sample BLE GATT server: `python gatt_server_example.py`

You can use a smartphone as a GATT client. I used the [GATT-IP](http://www.gatt-ip.org/) app, here it is on the [Google Play Store](https://play.google.com/store/apps/details?id=org.gatt_ip.activity&hl=en) and on the [App Store](https://itunes.apple.com/us/app/gatt-ip-bluetooth-smart-le-proxy-protocol/id940105344?mt=8)

![](http://jumper-public.s3-website.eu-central-1.amazonaws.com/gatt-ip.gif)

## License
The code in this repository is based on code taken from the [BlueZ](http://www.bluez.org/) project. It is licensed under GPL 2.0
