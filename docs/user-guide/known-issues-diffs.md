# Known Issues & Differences With Legacy Versions
As discussed in [What's New?](whats-new.md), AllStarLink v3 is
a gigantic leap forward in platform and software ecosystem. 
Many things are different in modern versions of Linux, Asterisk,
and more. This page documents permanent differences with ASL3
relative to legacy versions as well as any known issues that
must be fixed in ASL3.

## Differences with Legacy Versions

### Serial Port(s) Available by Default
On the ASL3 Pi Appliance, the system comes pre-configured
for `/dev/serial0` (formerly `/dev/ttyAMA0`) accessibility.
That means that Bluetooth and the default serial console
are disabled. Any directions requiring editing of `config.txt`
or `cmdline.txt` are unnecessary with the ASL3 appliance.

### Pi /dev Entry Changes
As ASL3 is based on Debian 12, users with Raspberry Pi devices must
note that the serial port on the Pi header is now `/dev/serial0`
rather than the historical `/dev/ttyAMA0`. If you are following
directions for Pi serial port operations, such as programming an
SA818/DRA818-based radio hat or a SHARI node, use 
`/dev/serial0` in place of the `/dev/ttyAMA0` reference.

### Voter/RTCM Default Port
Modern installations of Asterisk runs as the unprivileged `asterisk` user rather than
as `root`. Standard Linux convention prohibits non-root users to listen on a TCP
port below 1024. The default port for Voters/RTCMs has been changed to `1667` when
previously it was `667`. If voter port changes are difficult
for the environment, see [Incompatible Changes in ASL3](../adv-topics/incompatibles.md)
for other potential workarounds.

## Known Issues
The following issues are currently known to exist in AllStarLink 3 and,
where possible what the workarounds are.

### resize2fs_once "Error"
There are intermittent cases of errors on the screen or in 
the system logs about a failure of a service named 
`resize2fs_once.service` after the final first boot upon
installation. The error may report that it
"Failed to start" or "timed out". If the `/` partition has
been properly resized - which has been the case in every known 
occurrence of the error - then there is no action to take
and the issue will not appear on subsequent reboots.

A properly resized `/` should be a bit smaller than the full
size of the SD card or USB drive used with the device.
In Cockpit, look at the Storage tab:

![Known issue resize2fs](img/known_issue_resize2fs.png){width="600"}

In this example, `/` is a 31G partition on a 32G SD card.