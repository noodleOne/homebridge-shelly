# homebridge-shelly
[![NPM Version](https://img.shields.io/npm/v/homebridge-shelly.svg)](https://www.npmjs.com/package/homebridge-shelly)
[![Build Status](https://travis-ci.org/alexryd/homebridge-shelly.svg?branch=master)](https://travis-ci.org/alexryd/homebridge-shelly)

[Shelly](https://shelly.cloud) plugin for [Homebridge](https://homebridge.io),
enabling HomeKit support for Shelly devices.

## Supported devices
Currently the following devices are supported:
* [Shelly 1](https://shelly.cloud/shelly1-open-source/)
* [Shelly 1PM](https://shelly.cloud/shelly-1pm-wifi-smart-relay-home-automation/)
* Shelly 2 <sup>1</sup>
* [Shelly 2.5](https://shelly.cloud/shelly-25-wifi-smart-relay-roller-shutter-home-automation/) <sup>1</sup>
* [Shelly 4Pro](https://shelly.cloud/shelly-4-pro/)
* [Shelly Bulb](https://shelly.cloud/shelly-bulb/) <sup>2</sup>
* Shelly HD
* [Shelly H&T](https://shelly.cloud/shelly-humidity-and-temperature/)
* [Shelly Plug](https://shelly.cloud/shelly-plug/)
* [Shelly Plug S](https://shelly.cloud/shelly-plug-s/)
* [Shelly RGBW2](https://shelly.cloud/wifi-smart-shelly-rgbw-2/)
* [Shelly Sense](https://shelly.cloud/shelly-sense/)

### Notes
<sup>1</sup> To use Shelly 2 or Shelly 2.5 in roller shutter mode the device
must have been calibrated.

<sup>2</sup> Because of a bug in the Shelly firmware there is currently no
support for dimming the Shelly Bulb.

## Installation
1. Install homebridge by following
   [the instructions](https://www.npmjs.com/package/homebridge#installation).
2. Install this plugin by running `npm install -g homebridge-shelly`.
3. Add the configuration to your homebridge config.json.

## Configuration
In most cases, simply adding this plugin to the homebridge config.json will be
enough:
```json
"platforms": [
  {
    "platform": "Shelly",
    "name": "Shelly"
  }
]
```
Your Shelly devices will then be automatically discovered, as long as they are
on the same network and subnet as the device running homebridge.

### Network interface
Sometimes setting the `"networkInterface"` option to the local IP address of
your device will help when your devices aren't automatically discovered, or
you see error messages like `addMembership EADDRNOTAVAIL`.

### Authentication
Set the `"username"` and `"password"` options if you have restricted the web
interface with a username and password. Note that this configuration applies
to all Shelly devices.

### Request timeout
The `"requestTimeout"` option can be used to configure the timeout for HTTP
requests to the Shelly devices. Specify in milliseconds. Default is 10 seconds.

### Stale timeout
Use the `"staleTimeout"` option to configure how long a device can be offline
before it is regarded as stale and unregistered from HomeKit. Specify in
milliseconds. Default is 8 hours.

### Device specific configurations
Configurations for specific Shelly devices can be set using the `"devices"`
array. Each object in the array must contain an `"id"` property with the ID of
the Shelly device that you want to target. IDs are always made up of 6
hexadecimal characters and can be found in the Shelly Cloud app or the web
interface of a device, under *Settings -> Device info -> Device ID*.

#### General configurations
* `"exclude"` - set to `true` to exclude the device from Homebridge.
* `"username"` and `"password"` - set these if you have restricted the web
  interface of the device with a username and password. This will override the
  global `"username"` and `"password"` options.

#### Shelly RGBW2 configurations
* `"colorMode"` - set to `"rgbw"` (default) to have HomeKit control all four
  channels of the device (R, G, B, and W), or to `"rgb"` to omit the W channel.

#### Example configuration
```json
"platforms": [
  {
    "platform": "Shelly",
    "name": "Shelly",
    "devices": [
      { "id": "74B5A3", "exclude": true },
      { "id": "A612F0", "username": "admin", "password": "pa$$word" },
      { "id": "6A78BB", "colorMode": "rgb" }
    ]
  }
]
```

## Unsupported devices
If you have a Shelly device that is not yet supported by this plugin you can
help adding support for it by following these steps:

1. Run `$ homebridge-shelly describe <ip-address>` with the IP address of the
   Shelly device.
2. Create [a new issue](https://github.com/alexryd/homebridge-shelly/issues)
   and post the output from the previous command.

## Donations
I develop this plugin in my spare time. If you like it and you find it useful,
please consider donating a small amount by clicking the button below. That will
allow me to buy new Shelly devices so that I can add support for them.

[![Donate](https://www.paypalobjects.com/en_US/i/btn/btn_donate_LG.gif)](https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&hosted_button_id=P52VXJECUYTG8&source=url)
