# Known Issues
The following issues are currently known to exist in AllStarLink 3 and,
where possible, what work-arounds are.

## HTTP Registration

The new `rpt show registrations` command will show the status as registered if the password is wrong.

Workarounds are:

- Use the [AllStar Nodelist](https://allstarlink.org/nodelist) to validate registration.
- Or *CLI>`core set debug 10 res_rpt_http_registrations` to show registration status.
- Do *CLI>`core set debug 0 res_rpt_http_registrations` to disable debug.

## Pi Hat-based Radio Modules
For the ASL3 pi appliance image, the current image (v3.0.6) does not make
`/dev/ttyS0` available as a UART port for programming a hat-connected
radio board. This is a common need for hat-based modules based on the
SA818/DRA818 chip such as the W6IPA PIRIM and other similar board.

1. Run `sudo raspi-config` from the Web Console Terminal

2. Select **3 Interface Options***

3. Select **I5 Serial Port**

4. When asked "Would you like a login shell..." choose **NO**

5. When asked "Would you like the serial port hardware to be enabled?" choose **YES**

6. Select **OK**

7. Reboot when prompted - you MUST reboot for this configuration change
to become operable.

Note: With Debian 12, the onboard UART is no longer `/dev/ttyAMA0`
but is now `/dev/serial0`. Much older Pi documentation will still
(incorrectly) refer to `/dev/ttyAMA0` for the UART TTL port on the
Pi header.