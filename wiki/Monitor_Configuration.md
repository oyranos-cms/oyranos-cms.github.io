---
title: Monitor Configuration
permalink: wiki/Monitor_Configuration/
layout: wiki
tags:
 - Concepts
---

Monitor property control
------------------------

Modern monitors contain lots of control functionality. They interfere
with a proper calibration. So it is for some users useful to set them to
a state which coresponds to a certain ICC profile or disable such
settings at all.

If the properties are simple, they may be set to good defaults before
calirating such a display device. Some monitors provide higher than
8-bit per pixel LUT's, sometimes even for each colour channel. In this
case it is more promising to calibrate these LUT's directly and leave
the graphic cards LUT untouched. This help in providing more of the 256
steps possibly with todays VGA busses.

Possibly controls are brighness, contrast, LUT's, auto adjustment
features ...

Candiates for holding a according API are Xorg or HAL. Work is already
done in the ddccontrol project. Of course Xorg includes i2c
capabilities, which is under discussion to expose as a library.

### References

-   [1](http://www.ddccontrol.org)

<!-- -->

-   [Monitor Device Class
    Definition](http://www.usb.org/developers/hidpage/) at usb.org

<!-- -->

-   [Apple Cinema Display
    control](http://www.technocage.com/~caskey/acdctl)

