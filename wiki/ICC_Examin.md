---
title: ICC Examin
permalink: wiki/ICC_Examin/
layout: wiki
tags:
 - Oyranos
---

ICC Examin is a FLTK based colour profile viewer.

The educational purpose is to show the otherwise hidden internals of ICC
profiles and give users a rough estimation of the profiles quality.

Features
--------

-   see the [ICC
    Examin](http://www.behrmann.name/index.php?option=com_content&task=view&id=32&Itemid=1)
    page for an overview

Usage
-----

ICC Examin can be launched from the Application folder or Dock on Mac OS
X and from the Graphics menu on Linux.

### File opening

From the application windows menubar you can select File-&gt;Open to
show the file dialog. Select one or more files for gamut comparision as
you like. On top right side of the FLTK file selector resides the
bookmark alias Favourites button. If you frequently visit directories
you will find it usefull to append these directories to yout bookmark
list. To do this, go to an directory with the file selector and choose
from the bookmark button the add entry. The added directory appears in
the bookmark list and is available for later use.

You have selected one file and pressed ok. ICC Examin starts to parse
the file, showing the yellow progressbar. Depending on the complexity of
the file it may take some time to finish.

### Main window

Below the menu bar resides the tag list. It's entries are selectable.

You can select an tag from the taglist and watch its content in the tag
window below.

On bottom you see the status area of the window.

### Complex tags navigation

Some tags contain complex data. For such tags may appear a choicebutton
below the tag list. There you can select detailed views of a complex
tags endities.

### 3D navigation

To navigate arround in a 3D view use the:

-   left mouse button to rotate
-   middle mouse button or Shift+left mouse button to move/clip
-   right mouse button/ Strg+left button to obtain additional menus.
    Among the additional menus are in:
    -   top menu: the channel selection if appropriate
        -   Slice plane submenu, with axis slicing in fly through style
            and rotation
        -   Illustration submenu, with the background colour selection
            and text/marker switching off

### Windows and Views

#### Gamut

First to call is the 3D gamut viewer. You can select it from the menu
bar. It shows the gamut of the device described by the profile. If such
a description is not appropriate, the external used Argyll iccgamut
utility may not deliver a vrml gamut file and thus the 3D gamut view may
remain empty.

The colour space shown is allways in CIE\*Lab coordinates.

From the context menu (ctrl+left mouse or right mouse button) you can
select the average human (CIE standard observer) visible spectral
colours, as a line.

If meashurements are shown, theyre radius can be selected from the
context menu. This is handy to easily detect dE's of above 2 or 4. The
connection line goes from the measurement (white) to the deviation by
the profile (red).

ncl2 colour spots can be enlarged or made smaller by pressing + or -.

#### Report View

If the profile contains measurements a report is generated. You reach
this by selecting from the top menu View-&gt;Report. These measurement
data are compared to what is calculated with the profile by littleCMS -
the internal used CMM.

Such a comparision from device colours + measurements colours on the one
side and device + profile/CMM colours on the other side are just one
possible quality checking method.

More comparision styles would be nice, in giving better meaning for
varying criteria. The differences are summarised in the reports top
lines. Each like contains the the colour values and euclidian dE +
dE2000. Two rectangles on the right side may help to see the colour
differences visually. The first monitor profile is used for this.

The report can be exported from the File menu in html format.

#### CGATS view

The measurement data is taken from the profile, if available, and
transformed to fit in the CGATS standard. A window can be called from
the View menu to show the corrected measurement output.

#### Grafic card gamma tables

The gamma tables in the grafic card are shown in an external window,
callable from the View menu. It shows on osX/XFree86/Xorg the RGB
curves. The monitor profile can be loaded from this window in the main
profile viewer window for further examination.

Under Linux Oyranos support must be compiled in to do so.

#### Help

The Help menus About button shows a short overview, license and other
programers acknowledgement, who helped with providing theyre code for
free.

Profile elements
----------------

### Header

Now you see the tag list has obtained some entries, showing the profiles
tags. The first entry is allways the header. If the header is selected
the tag window below shows many useful information about the profile.
Among these information are:

-   the internal stored size of the profile
-   the prefered ColourMatchingModule (CMM)
-   ICC standard version
-   kind of usage
-   device colour space
-   the internal used reference colour space
-   date of creation
-   file type sinature (allways acsp)
-   and some more or less meaningfull informations

### Tags

Below the header, which behaves like a fixed tag, are the variable tags
listed. They appear in the same order as in the file. Starting withe the
tag number, then the tag signature and the type of content in the tag.
The size of the tag follows and a small description gives you an idea af
what the tag may be intended for.

#### text / desc / targ

Tags of type text are the most simple ones. they include informations
about the profile like License informations, Description for displaying
on behalf of the whole profile, Measurement data , in CGATS text formet
and more.

#### curv

An other type are curves. They are shown as such. Note the coordinates
are all normalised to 0.0 -&gt; 1.0.

#### XYZ

XYZ tags show things like Mediawhitepoint or Primaries of monitors in
the CIE\*xy diagram.

Note: primaries and some curves are grouped to better understand theyr
meaning in the profile.

#### mft1 / mft2

MFT1/2 tags are complex and contain a set of peaces to do a colour
transformation. The choice button below the tag view names them. You can
select the matrix, in-and output curves and the CLUT. Currently only
CLUTs with less than 3 dimensions in input direction are supported. This
kind of tag is mostly independend of other tags. Only few tags like wtpt
and chad may influence them.

The CLUT view has various options to visualise the table. For instance
you can make table appear coloured or select a channel of choice. The
numbers in the status window are normalised to 0.0 -&gt; 1.0.

They contain the result of hard work in researching the best translation
of scattered measurements to equally spaced grid tables. Only this step
makes colour transformation reasonably fast.

The tag is described in in verson 2 of the ICC specification. In ICC
specification version 4 a new even more complex tag is introduced and is
calleed mAB.

#### sf32

sf32 and similiar tags may contain only numbers. Theyre interpretation
depends on the name of the tag. For instance the tag named chad is used
to specify a colour transformation matrix, which was originally used to
normalise the measured colours to D50 standard conditions.

#### ncl2

The ncl2 tag is used to store named colours in a list. This can be used
to describe spot colours or describe a painters palette. Loading a
profile containing such a tag into ICC Examin switches the 3D gamut view
mode on. You see then the colours in 3D (CIE\*Lab) and not as a list of
numbers as in the tag viewer.

More tags can follow here...

Other file formats
------------------

### CGATS

Measurement data in CGATS format can be opened in ICC Examin. In the
file selector is a dedicated filter available. The data are shown as
text and in the 3D view.

### VRML

A subset of vrml alias wrl files is parsed. It allowes to open colour
gamuts produced with argyll and saved with ICC Examin.

It would be nice to allow as well lines to get parsed, which are used
for visualisations by iccview for instance.

Preferences
-----------

### Language support on BSD

On BSD systems you must set shell environment variables. For instance in
/etc/profile or $HOME/.profile:

`LANG=de_DE.ISO8859-1; export LANG`  
`MM_CHARSET=ISO-8859-1; export MM_CHARSET`

See further [FreeBSD german i18n
description](http://www.freebsd.org/doc/de_DE.ISO8859-1/books/handbook/using-localization.html)
