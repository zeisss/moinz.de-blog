+++
date = "2017-09-06T20:00:00+02:00"
title = "Controlling the TV with my Raspberry PI"
description = ""
+++

Just so I find this my self again the future:

Install `cec-utils` which contains the `cec-client`.


# Turn on
```
echo "on 0" | cec-client -s -d 1
```

Turns the TV on.

# Switch channel

```
echo "as" | cec-client -s -d 1
```

Switches the TV to the Raspberry PI.

# Turning off

```
echo "standby 0" | cec-client -s -d 1
```

Turns the TV off. To make this work with my Samsung I had to enable this in the TV settings.

# Read the status

```
$ echo "pow 0" | cec-client -s  -d 1
opening a connection to the CEC adapter...
power status: standby
```

# Notes

 * `-d 1` - Turns off a lot of output, `cec-client` is by default quite noisy
 * `-s` - Single command mode - quits the client after sending the command
 * `0` - The 0 in the command refers to the TV. Use `scan` to list all devices