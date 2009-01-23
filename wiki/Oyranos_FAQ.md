---
title: Oyranos/FAQ
permalink: wiki/Oyranos/FAQ/
layout: wiki
tags:
 - Oyranos
---

Even most questions are answered on the
[Oyranos](http://www.oyranos.org) site already, here is the FAQ.

If you have the impression an important question is missed, feel free to
add it.

### What is Oyranos?

The Oyranos project is a colour management system (CMS). It is intended
to work in a comparable fashion like KCMS, ICM or ColourSync except it
is published with sources and is available for various platforms.

### What is the goal of Oyranos?

Oyranos tries to provide colour management services for applications and
services like Scribus, CinePaint, Krita, Gimp, Inkscape, Gutenprint,
UFraw, Cups, Xorg, Sane and so on.

With colour management being a often complicated pattern, the need rises
to easily understand what goes on behind the scenes. Doing this once is
often hard enough. Having different colour settings in every application
and service may easily multiply the work to relyable understand how
colours get managed. Thus Oyranos is a call to collaborate between
applications to make them all more attractive.

For instance all Oyranos conform applications should display colour
content on the monitor in the same manner, equally if the user has set
soft proofing on by default in the Oyranos configuration panel or not.

### Where comes the name Oyranos from?

Oyranos is the greek word of sky.

It was pointed out that ouranos is more adequate for english readers.
Just as with the german Uranos and other variants it seems pretty good
to stay with the name.

### License(s)

Oyranos is licensed under [new
BSD](http://opensource.org/licenses/bsd-license.php). It is possible
that parts will be released under different licenses. But that is open.
The goal is to not exclude anyone from using Oyranos. The ICC profiles
are licensed, except a few, under
[zip/libpng](http://opensource.org/licenses/zlib-license.php) license.

### Where can I get Oyranos?

Oyranos is officially published on
[Oyranos/Download](/wiki/Oyranos/Download "wikilink").

### Where Can I find ICC Profiles

Some are already included in the package, like sRGB, ECI- and a Adobe
RGB as well as Gray, CIE\*Lab, CIE\*XYZ, ITU-Lab and some press profiles
like for FOGRA, SWOP, SNAP and GRACoL printing conditions. The used
printing condition character sets are as well included. More profiles
can be found on this [link
collection](http://www.behrmann.name/index.php?option=com_weblinks&catid=73&Itemid=95).

### Who is developing Oyranos?

Currently Oyranos is a one man project of [Kai-Uwe
Behrmann](http://www.behrmann.name). I see myself as a photographer, who
came in the situation of creating its own imaging workflow through the
lack of adequate GUI's on the Linux OS. Still I am searching for
[help](#How_can_I_help_with_the_Oyranos_CMS.3F "wikilink").
Contributions came from students through their
[Summer](http://www.freedesktop.org/wiki/OpenIcc/ColorManagementNearX)
of
[Code](http://code.google.com/p/google-summer-of-code-2008-openicc/downloads/list)
[projects](http://freedesktop.org/wiki/OpenIccForGoogleSoC2008) at
[OpenICC](/wiki/OpenICC "wikilink").

### How can I help with the Oyranos CMS?

You could help by testing, reporting bugs or providing according
patches, doing translations, as well as suggesting useful changes or
becoming part of the development team.

We need people with fantasy for going possibly new paths, meticulousness
for assuring quality, analytical, didactic and aesthetic skills and
thinking around the corner or all together. Some knowledge or feeling of
colour may be of help. But this is not a must, as uneducated persons
bring in a very important view.

See as well [here](/wiki/Oyranos#Development "wikilink").

### Which applications use Oyranos?

A list of Oyranos users is [here](http://www.oyranos.org/#audience).

A list of Linux/BSD relevant colour managed applications can be found
[here](http://www.oyranos.org/wiki/index.php?title=Applications).

### Can Oyranos replace other Colour management Systems?

This is not intentional. Each colour management system has its strengths
not easily reachable by an other. If your application runs just on osX
it is possibly best to stay with the advanced features of ColourSync. Is
your intention to run your application on different platforms such as
Windows, osX and the various unixes, Oyranos may be of much value, as it
will provide a single API allowing real cross platform development.
Oyranos tries to use as many as possible of the underlying colour
management services, as long as it conforms to its cross platform
behaviour.

Naturally advanced features will be unlikely to get supported as they
are not cross platform, and would have to been accessed directly.

[back -&gt; Oyranos](/wiki/Oyranos "wikilink")
