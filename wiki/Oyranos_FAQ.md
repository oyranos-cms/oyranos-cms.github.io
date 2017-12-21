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

Oyranos shall help in making end to end colour management working for
open source operating systems. Ideally that works for most users without
intervention.

With colour management being a often complicated pattern, the need rises
to easily understand what goes on behind the scenes. Doing this once is
often hard enough. Having different colour settings in every application
and service may easily multiply the work to reliable understand how
colours get managed. Thus Oyranos is a call to collaborate between
applications to make them all more attractive.

For instance all Oyranos conform applications should display colour
content on the monitor in the same manner, equally if the user has set
soft proofing on by default in the Oyranos configuration panel or not.

Oyranos provides colour management services for desktops, applications
and services like KDE, Gnome, Scribus, CinePaint, Krita, Gimp, Inkscape,
Gutenprint, UFraw, Cups, Xorg, Sane and so on.

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
are licensed under
[zip/libpng](http://opensource.org/licenses/zlib-license.php) license.
They are separately packaged in the OpenICC-data package.

### Where can I get Oyranos?

Oyranos is officially published on
[Oyranos/Download](/wiki/Oyranos/Download "wikilink").

### Where Can I find ICC Profiles

Some are already packaged in OpenICC on www.sourceforge.net, like sRGB,
ECI- and a Adobe RGB as well as Gray, CIE\*Lab, CIE\*XYZ, ITU-Lab and
some press profiles like for FOGRA, SWOP, SNAP and GRACoL printing
conditions. The used printing condition character sets are as well
included. More profiles can be found on this [link
collection](http://www.behrmann.name/index.php?option=com_weblinks&catid=73&Itemid=95).
They should be installed in the [system
paths](/wiki/OpenIccDirectoryProposal "wikilink") to be seen by most
applications.

### Who is developing Oyranos?

Oyranos was started by [Kai-Uwe Behrmann](http://www.behrmann.name).
Yiannis Belias has joined. More details can be read in the AUTHORS file
in the sources. Still we are searching for
[help](#How_can_I_help_with_the_Oyranos_CMS.3F "wikilink"). Code
contributions came from students through their
[Summer](http://www.freedesktop.org/wiki/OpenIcc/ColorManagementNearX)
of
[Code](http://code.google.com/p/google-summer-of-code-2008-openicc/downloads/list)
[projects](http://freedesktop.org/wiki/OpenIccForGoogleSoC2008) at
[OpenICC](/wiki/OpenICC "wikilink"). OpenICC people help very much around
organisation of GSoC.

### How can I help with the Oyranos CMS?

You could help by testing,

-   reporting bugs or
-   providing according patches,
-   doing translations,
-   suggesting useful changes or
-   proofreading, updating and extenting the documentation or
-   write a tutorial on installing and using or
-   package Oyranos, the OpenICC profiles and the other depending
    projects

Becoming part of the development team is easy, just ask.

We need people with fantasy for going possibly new paths, meticulousness
for assuring quality, analytical, didactic and aesthetic skills and
thinking around the corner or all together. Ideally Oyranos shall be
invisible to most users and simply work for their colour devices. So if
your have a question around Oyranos thats a good sign to start ask that.

See as well [here](/wiki/Oyranos#Development "wikilink").

A TODO list can be found [here](/wiki/Oyranos/FeatureWish "wikilink"). More
project ideas can be found on the [OpenICC GSoC
pages](http://www.freedesktop.org/wiki/OpenIcc/GoogleSoC2009).

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

### Does Oyranos rely on FLTK?

Oyranos comes with a front end GUI written in FLTK. However building
that can be switched off during configuration, in case a desktop decides
to have a equivalent or better replacement as front end. E.g. KDE might
ship the [KolorManager](http://www.oyranos.org/kolor-manager) front end
to Oyranos instead. A Gtk front end would be great too.

### Elektra dictates the core design?

No. Elektra provides just a API to store settings in a data base. Thats
a very common task and available through gconf or the Qt framework. But
Elektra is cross desktop. The Elektra API calls are abstracted in
Oyranos. So Elektra could be replaced by an other desktop independent
configuration engine. But as the Elektra project sees continuing
development there is currently no reason. It is planed to formalise
settings storage and share that among CMS's.

### Elektra is a lively project?

As of writing, in 2011, Elektra exists after more than 5 years
continually development. The noise on email lists is not very loud, but
there is academic interest and industry use for Elektra. Its a small and
specialised project with a very focused problem to solve. Thus is is not
uncommon to see fewer comments around the project.

### What about “Mixing the configuration, with the UI, with the back end.”?

You guess it right. This statement is nonsense. Configuration, UI and
back ends are very well separated. E.g. you do not need to call into a
toolkit to access the configuration data base. oyranos-policy as a
command line tool is an examples for not relying on Xorg to be usable.

### What about “Reliance on compiz for full screen color management.”?

The compiz ICC colour server is at the time of writing the only
available open source solution to allow colour management across the
full desktop on multiple monitors. So naturally it is recommended,
because it is technical superior to most other desktop colour correction
strategies. E.g. The loading or the 'vcgt' tag is only a calibration,
which helps not much with wide gamut displays. However the underlying
net-color spec is open and free to be implemented in say Xorg.

### Why has Oyranos a own type and object system?

The decision came as we realised the project needs some efficient way to
manage its internal objects and classes alike structures. As the
selected programming language comes with no explicit support for that it
was written from scratch. We looked as well on other systems for
instance Glib. But we found that the language extension for inheritance
and so on where realised outside of the core C language specification in
a Macro called second language, which is commonly referred to as bad
style programming. So Glib would have come with lots of disadvantages.

### What about “No distribution is planning to ship elektra or Oyranos.”?

Many distributions plan or have considered shipping Oyranos. Like Fedora
does since years.

[back -&gt; Oyranos](/wiki/Oyranos "wikilink")
