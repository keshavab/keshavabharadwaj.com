+++
comments = true
date = 2014-03-07T00:00:00Z
title = "TP-Link MR3020 and ZTE MF 825A - Making it work"
description = "Making the TP-link nano router work with airtel 4g dongle."
+++

You have got ZTE MF 825A ( 4G dongle, typically in india with airtel)
and have bought TP-Link MR3020 to enjoy 4g speed over wifi. and oops.. they are not working out of the box. You are not alone. There are lotsa people including me facing same problem. Below are things you can do to make them work.

Problem:
March 07 2014.
As on this date, TP-Link MR3020 ships by default with firmware revision with 9/29/2013. On connecting ZTE MF 825A with this, it did not work. i.e modem status says identified. but connection to 4g network never succeeds. Hence out of the Box, MF825A doesnot work.
The latest version on website is the same version - 9/29/2013. That doesnot serve no good.

Solution:
In comes the saviour - [Openwrt](http://en.wikipedia.org/wiki/OpenWrt).
OpenWrt is described as a Linux distribution for embedded devices.

1. Browse to [http://ofmodemsandmen.com/downloads.html](http://ofmodemsandmen.com/downloads.html). This provides firmware out of box based on openwrt.
2. Choose the huntsman version for 3020 which is the stable version. download this firmware bin file.
3. login to router admin url. 192.168.0.254.  click on firmware section. click on upgrade.
4. choose the bin file downloaded earlier and click on upgrade.
5. once upgrade is clicked, the router applies the above firmware and reboots. on reboot you would be welcomed with a new screen which are screens of openwrt and not of tplink. This may void the warranty and do it at your own risk.
6. Now login to same admin url. - 192.168.0.254 or 192.168.1.1 now click on modem->connection section.
7. Enter these values -
   APN: airtelgprs.com
   pin: *99#

Reboot the router and start enjoying high speed 4g over wireless.
Enjoy !!!!

P.S: Read the instructions once on openwrt before flashing the firmware.
