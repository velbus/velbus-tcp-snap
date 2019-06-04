# velbus-tcp-snap

Snap package for python-velbustcp

## Connect serial/USB interface

```
:warning: Not connecting the interface will cause the program to not function. :warning:
```

To allow the snap to access your Velbus USB interface, connect it to the raw-usb plug using

`snap connect velbus-tcp:raw-usb :raw-usb`

Alternatively, if you are running on a gadget which exposes a serial-port slot, use

`snap connect velbus-tcp:serial-port :serial-port`

## Auto discovery

By default, the application will connect to the first Velbus USB interface it can find and use. If you want to change this behaviour, you can manually set the port using

`snap set velbus-tcp serial.autodiscover=false`  
`snap set velbus-tcp serial.port=/dev/ttyACM0`

## Authorization

You can enable authorization to restrict outside access to your Velbus installation, enable it by using

`snap set velbus-tcp tcp.auth=true`

By default, an authorization key is generated during installation, to get this key use

`snap get velbus-tcp tcp.authkey`

To set the authorization key, use

`snap set velbus-tcp tcp.authkey=YOUR_KEY_HERE`

## SSL

You can enable SSL to encrypt the connection between you and your Velbus installation, enable it by using

`snap set velbus-tcp tcp.ssl=true`

By default, a certificate is generated during installation. If you want to supply your own certificate, use

`snap set velbus-tcp tcp.cert=PATH_TO_YOUR_CERTIFICATE`  
`snap set velbus-tcp tcp.pk=PATH_TO_YOUR_PRIVATE_KEY`

## Configuration

All configuration options

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