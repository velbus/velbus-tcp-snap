# velbus-tcp-snap

Snap package for python-velbustcp

## Connect interface and set port

To connect the usb interface, use either

snap connect velbus-tcp:raw-usb :raw-usb

or

snap connect velbus-tcp:serial-port :serial-port


Autodiscovery wil not work, to manually set the port use

snap set velbus-tcp serial.port=/dev/ttyACM0

 

## Configuration

To change the configuration use

```
snap set velbus-tcp tcp.port
snap set velbus-tcp tcp.relay
snap set velbus-tcp tcp.ssl
snap set velbus-tcp tcp.cert
snap set velbus-tcp tcp.pk
snap set velbus-tcp tcp.auth
snap set velbus-tcp tcp.authkey
snap set velbus-tcp serial.autodiscover
snap set velbus-tcp serial.port
snap set velbus-tcp logging.type
snap set velbus-tcp logging.output
```