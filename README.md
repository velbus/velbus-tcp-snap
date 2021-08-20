# velbus-tcp-snap

[![velbus-tcp](https://snapcraft.io/velbus-tcp/badge.svg)](https://snapcraft.io/velbus-tcp)

Snap package for [python-velbustcp](https://github.com/velbus/python-velbustcp).

## Installation

### Install from snap store

The snap is published through the official Canonical snap store. To install, simply open a terminal on any snapd-supported Linux distribution and type:

```yaml
snap install velbus-tcp
```

### Connecting the interface

:warning: Not connecting the interface will cause the connection to the bus to fail :warning:

To allow the snap to access your Velbus USB interface, connect it to the raw-usb plug using:

```yaml
snap connect velbus-tcp:raw-usb :raw-usb
```

Alternatively, if you are running on a gadget which exposes a serial-port slot, use:

```yaml
snap connect velbus-tcp:serial-port :serial-port
```

## Configuration

A complete list of configuration options is listed below. The current configuration can be retrieved with:

```yaml
snap get velbus-tcp -d
```

### Serial

By default, the application will connect to the first Velbus USB interface it can find and use (based on VID and PID). If you want to change this behaviour or use a serial port, you can manually set the port using:

```yaml
snap set velbus-tcp serial.autodiscover=false  
snap set velbus-tcp serial.port=/dev/ttyAMA0
```

### TCP binding

By default, the application will bind on 27015 and accept all hosts, using TLS/SSL and authorization.

#### Authorization

You can enable/disable authorization to restrict unauthorized access to your Velbus installation by using:

```yaml
snap set velbus-tcp tcp.auth=true
```

By default, an authorization key is generated during installation, to get this key use:

```yaml
snap get velbus-tcp tcp.authkey
```

To set your own authorization key, use:

```yaml
snap set velbus-tcp tcp.authkey=YOUR_KEY_HERE
```

The authorization key is a key that needs to be sent after establishing a connection. No data will be exchanged until the key verified.

#### TLS/SSL

You can enable TLS/SSL to encrypt the connection between you and the application:

```yaml
snap set velbus-tcp tcp.ssl=true
```

The used certificate can be found at `/var/snap/velbus-tcp/common/`.

#### Multiple bind points

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

#### NTP

The application can broadcast the system time on the bus, this is option disabled by default.

You can enable NTP with:

```yaml
snap set velbus-tcp ntp.enabled=true
```

When enabled, it will broadcast the time at startup, after that;

If ntp.synctime is not set or is set to empty, it will do so at every hour transition and at DST transitions, whichever is closer.

If ntp.synctime is set, it will broadcast at the specified time and at DST transitions, whichever is closer.

To change the the sync time use

```yaml
snap set velbus-tcp ntp.synctime='03:00'
```

## Logging

The application logs can be obtained using:

```yaml
snap logs velbus-tcp -f
```

To set the verbosity level (info, debug) of the logging:

```yaml
snap set velbus-tcp logging.level=debug
```

## Troubleshooting

Having troubles getting the snap up and running?

Ensure the plug is [connected](#Connecting-the-plugs), otherwise USB/serial communication will not work.

Try to disect the [logging](#Logging) for possible errors.

Try installing the core snap with:

```yaml
snap install core
```