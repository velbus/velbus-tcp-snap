# velbus-tcp-snap

[![velbus-tcp](https://snapcraft.io/velbus-tcp/badge.svg)](https://snapcraft.io/velbus-tcp)

Snap package for python-velbustcp

## Installation

The snap is published through the official Canonical store. To install simply open a terminal on any snapd-supported Linux distribution and type

`snap install velbus-tcp`

## Connect serial/USB interface

:warning: Not connecting the interface will cause the connection to the bus to fail :warning:

To allow the snap to access your Velbus USB interface, connect it to the raw-usb plug using

`snap connect velbus-tcp:raw-usb :raw-usb`

Alternatively, if you are running on a gadget which exposes a serial-port slot, use

`snap connect velbus-tcp:serial-port :serial-port`

## Auto discovery

By default, the application will connect to the first Velbus USB interface it can find and use. If you want to change this behaviour or use a serial port, you can manually set the port using

```yaml
snap set velbus-tcp serial.autodiscover=false  
snap set velbus-tcp serial.port=/dev/ttyAMA0
```

## NTP

The application can broadcast the system time on the bus, this is option disabled by default.

You can enable/disable NTP by using

`snap set velbus-tcp ntp.enabled=true|false`

When enabled, it will broadcast the time at startup, after that;

If ntp.synctime is not set or is set to empty, it will do so at every hour transition and at DST transitions, whichever is closer.

If ntp.synctime is set, it will broadcast at the specified time and at DST transitions, whichever is closer.

To change the the sync time use

`snap set velbus-tcp ntp.synctime='03:00'|''`

## TCP binding

By default, the application will bind on 27015 and accept all hosts, using SSL and authorization.

## Authorization

You can enable/disable authorization to restrict unauthorized access to your Velbus installation by using

`snap set velbus-tcp tcp.auth=true|false`

By default, an authorization key is generated during installation, to get this key use

`snap get velbus-tcp tcp.authkey`

To set your own authorization key, use

`snap set velbus-tcp tcp.authkey=YOUR_KEY_HERE`

The authorization key is a key that needs to be sent after establishing a connection. No data will be exchanged until the key verified.

## SSL

You can enable SSL to encrypt the connection between you and the application, enable/disable it by using

`snap set velbus-tcp tcp.ssl=true|false`

## Multiple bind points

You can set up multiple bind points by using comma-seperated values. You'll need to supply all values for a second bind point, for example;

```yaml
snap set velbus-tcp \
tcp.host=0.0.0.0,127.0.0.1 \
tcp.port=27015,54934 \
tcp.relay=true,true \
tcp.ssl=true,true \
tcp.auth=true,false \
tcp.authkey=MY_AUTH_KEY,
```

Which would set up two bind points;

One which binds on 27015 and accepts all hosts (0.0.0.0), which has TCP relay and SSL and uses auth with MY_AUTH_KEY
One which binds on 54934 and only accepts 127.0.0.1, which has relay and SSL and doesn't have auth

## Configuration

All configuration options

```yaml
snap set velbus-tcp velbus.ntp
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
