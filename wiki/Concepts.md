---
title: Concepts
permalink: wiki/Concepts/
layout: wiki
---

**Concepts** which shall help ensuring interoperatibility, ease of
interaction or meet other goals. They should serve the end to end
expectations of users. Pros and Cons can be discussed here.

Diversity
---------

To bring various users and producers together the
ICC[1](http://www.color.org) standard was created. This standard covers
a data format to exchange colour information of devices.

Precision
---------

The OpenEXR CTL[2](http://www.openexr.com/documentation.html) approach
to use direct colour formulas in GPU shader programs is an try to
increase precision and speed related to the demands of the film industry
[3](http://www.ilm.com).

Consistency
-----------

Editing spaces are a very valuable concept to achive good results during
compositing and manipulating images.

-   colour channels should by equally editing the exposure, behave
    equally regarding saturation (no turning of gray into green)

Flatcolor vs. mixed mode documents
----------------------------------

One concept of the ICC-standard, is the possibility to create documents,
where every object (image, vectorgraphics, text-objects) can have is own
profile and rendering intent. This makes colormanagement of complete
documents very complex and can easily results to unwanted
colortransformations of individual objects of an document. To give users
succesful experiences with colormanagement, it is useful to have the
option of an colormanagement policy, which allows only the creation of
flatcolor documents in well known and tested editing spaces.

Stages of manipulation
----------------------

Handling of colour data is been expected in serveral states, handled by
dedicated colour spaces. The following describes a process with three
steps.

-   know data (tagged with profile or machine readable description),
    unknown or uncertain data -&gt; assign a assumed source profile
    (distinguish RGB / Cmyk)
-   editing colour space to tweak and manipulate, mostly with enough
    colour volume
-   output or proofing colour space, considered as a destination for the
    final content. This colour space can be used to check against during
    editing and possibly convert as the last stage of editing.

Untaged data
------------

Most difficult is here the mixed behaviour of applications regarding
tagging versus non tagging of exchange data with colour profiles.

### Assign an profile into untagged data

A simple example is a photographer, which is aware of tagging images
correctly and delivers them to his customer. Next step is to include
such tagged photo into an document in an CM unaware word processor. The
output from the word processor is prepared as pdf for the web and as pdf
for printing. As the word processor is ignoring any colour profiles it
is up to the system to follow a rule, which makes the colour data
unambiguous.

-   leave it as is for viewing, and interprete as follows below
    -   pos:
        -   signal that untagged data are unknown
    -   cons:
        -   ambiguous across platforms
-   attach only during modifications - maybe convert to an default
    colour space (is policy dependent)

### Interpretation of untagged data

-   always sRGB, the [WWW](/wiki/Standards#sRGB_workflow "wikilink") standard
    colour space
    -   pros:
        -   mostly unambiguous
    -   cons:
        -   sRGB is limited regarding saturation
-   always osX standard RGB ??
-   always Adobe RGB(1998) ??
-   take data as in monitor colour space - a traditional point of view
    used up to date
-   differentiate between input path for colour data:
    -   WWW sites -&gt; sRGB
    -   Files from outside of the computer -&gt; selectable profile
    -   Files from inside the computer -&gt; selectable profile

As the source of images, whether they come from out- or inside the
computer, becomes more and more fuzzy, this concept is difficult to
implement.

### Save onto an untaggable image format

-   warn user about losing colour space information during saving

Policies
--------

### Average User

Most people belong to the [Office User
type](/wiki/What_the_users_want#Office_Users_.2F_Webdesigners "wikilink").
They need an reliable conversion behaviour. Simplicity is the main goal
there. [sRGB](/wiki/Standards "wikilink") serves this behaviour well. Defaults
should be set to:

-   assumed RGB - sRGB
-   editing colour space: sRGB
-   convert allways data to editing space (before a save, not nice, but
    the most reliable in mixed CM aware environments)
-   dont prefere mixed colour space documents (keep it simple)

### Graphics Distribution

[Graphic Designers](/wiki/What_the_users_want#Graphic_Designers "wikilink")
and other specialist may want to use own settings. Here some defaults:

-   assumed RGB - sRGB or Adobe(?)
-   no popup for untagged images
-   editing RGB - Adobe,ECI or L-Star (large gamut)
-   convert RGB data during editing to editing space (dont pop up
    dialogs)
-   no popup for conversion
-   dont convert CMYK data (because of possibly failed black preserving
    capabilities)
-   allow mixed colour space documents (warning for internet PDF's?)

Device Settings
---------------

The device to device colour path contains as well the settings to
receive and to output colours. This makes the storage of these settings
necessary for a working colour management. Currently such settings are
spread over various places. They are particially stored in application
and OS databases or only particially embedded in profiles, like the vcgt
tag. There should be a format developed and used, which makes it easy to
combine both colour and settings characterisation.

[Device Settings](/wiki/Device_Settings "wikilink")

User Interface
--------------

### Profile Selection

-   use a flat directory to store all files
    -   easy to read by all applications
    -   needs several mechanims to distinguish profiles for devices,
        editing ...
-   use directories hierarchically
    -   allow all kind of distinguishing even if not supported by
        Oyranos, other may use nevertheless
    -   easy grouping of device, editing ... profiles
    -   needs a layout and specification

