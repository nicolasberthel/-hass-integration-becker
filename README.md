# Becker cover support for Home Assistant

A native home assistant component to control becker RF shutters with a Becker Centronic USB Stick.
It uses [pybecker](https://pypi.org/project/pybecker/).
The becker integration currently support to
- Open a Cover
- Close a Cover
- Stop a Cover

It as well support value template if you wan to use sensors to set the current state of your cover


## Installation

Copy the different sources in custom_components folder of your hass configuration directory

## Configuration

Once installed you can add a new cover configuration in your HA configuration

```yaml
becker:
  device: "/dev/serial/by-id/usb-BECKER-ANTRIEBE_GmbH_CDC_RS232_v125_Centronic-if00"
  covers:
    - name: "Kitchen Cover"
      channel: "1"
    - name: "Bedroom Cover"
      channel: "2"
      value_template: "{{ states('sensor.bedroom_sensor_value') | float > 22 }}"
```

Note: The channel needs to be a string!

The configuration of the centronic device can be done as well via the integration configuration screen

## Note

The component does not support pairing for the moment. It means that your different shuters must be already paired with your USB stick
You can achieve this prior to the installation in home assistant by using [pybecker](https://pypi.org/project/pybecker/) with the following command
Of course you have to put your shutter in pairing mode before. This is generally done by holding the programming button of your sender until you hear a "clac" noise

```
pybecker -a PAIR -c <CHANNEL_ID>
```

### EDIT

Thanks to [markbergsma](https://github.com/markbergsma) pairing is now possible from the UI, a script or an automation using the fresh new *becker.pair* service. This requires channel and a unit as parameter.

## Support

[![Donate](https://img.shields.io/badge/Donate-PayPal-green.svg)](https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&hosted_button_id=Q7A292QK8Z7BW&source=url)

This integration was developed for my home integration. Even if I tried to make it as generic as possible, it could be that you have to adapt it a bit for your own integration.