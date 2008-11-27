---
title: Concepts
permalink: wiki/Concepts/
layout: wiki
tags:
 - Concepts
---

Abstract
--------

**Concepts** which shall help ensuring interoperability, ease of
interaction or meet other goals. They should serve the end to end
expectations of users. Pros and Cons can be discussed here.

In parts this sketchy page picks up concepts, provides relevant
examples, lists pros and cons and analyses available systems. If you
feel this all should be more structurised I havily agree. Just most
often developers are hanging in details or implementations or simply
have the picture in their mind. This page is dedicated to the public, so
everyone should be able to read and understand it. If not edit and
rearrange this page or if unshure ask questions on the backside (see
link “discussion” above).

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

An other high precision CMM exists with
[SampleICC](/wiki/ColourMatchingModuls#SampleICC "wikilink") from ICC.

Consistency
-----------

“Editing Spaces” are a very valuable concept to achieve good results
during compositing and manipulating images.

-   colour channels should by equally editing the exposure, behave
    equally regarding saturation (no turning of gray into green)

In an architectural sense consistency means to include all parties to
colour manage.

-   It makes sense to search for the most common used parts or API's and
    plug-in there colour management in order to hit all at once.
-   an other strategy might be to establish rules, which all parties
    should apply to. But thats not so easy to get them all, as many
    applications or toolkits might simply not be interested in the first
    place.
-   a thierd path is to provide the means for tracking colour
    conversions

### History tracking for colour conversions

-   embed profile ID's into DL's (done - psid)
-   export colour conversions as DL's (done - is a CMM backend API
    requirement)
-   embed DL's into the output profile
    API:oyColourConversion\_OutputProfile()
-   optional e.g. oyProfile\_OptionSet( “history\_tracking” )
-   examine tools - on screen (compiz?)

### Embedding of Rendering Intents

Typical rendering intents are selected during the colour conversion or
retrieved automatically. The imagery has no such information. A ICC
profile flag for the rendering intent is in most cases ignored.
Nethertheless there might be some situtations, where selecting a
rendering intent can have advantages. These are:

-   passing a rendering intent through a unknown transport mechanism to
    a end conversion, e.g. a device driver
-   advice handle certain colour areas of a media independent document
    in a specific way, e.g. images (perceptual) and logo (relative
    colourimetric) colours combined in a PDF

Nethertheless as the rendering intent is dependent to the colour
context, e.g. surrounding colour elements, embedding a advice for a
rendering intent should be used only for certain cases. By specifying
the rendering intent in a too early state, the later colour conversions
might be over specified and thus ending in conflicts.

Flexibility
-----------

### Static colour spaces

One example is the assumtion that monitors are in sRGB and all colour
delivered to the system must be in that colour space. This is largely
for Linux/BSD (2007) the case.

An other great example is the Microsoft pre Vista colour management
policy to tread all input and output as sRGB.

### Variable colour spaces

In a system allowing to assign or recognise to each colour device a
separate profile features great flexibility. Apples ColourSync is a good
example for that. Other systems follow this general approach.

### Influencing the CMMs

#### Apple and the ColorSync control panel options

osX has times ago options in its ColorSync control panel. These
dissappeared as Apple understood that most applications use their own
settings. This was blamed later on as the reason for much confusion. To
better understand, ColorSync refuses to enforce options.

#### Oyranos options system

In opposite to ColorSync Oyranos provides a pre configured colour
conversion object, in terms of ColourSync a Colour World. The Oyranos
colour conversion object defaults usually to the settings from the
system control panel.

To modify settings a application will have to ask for a options object.
This should reflect the preconfigured settings of eighter the system or
the application.

This Options can be presented to the user and will contain as well CMM
specific options. Thus it will be possible to allow additional features
and unconventional behaviour enabling and configuration.

To allow for arbitrary options in a flexible way, a layer must be
established to provide logic, data (settings) and basic layout of the
options in a toolkit independent way. Basically the CMM should not care
nor link against a special toolkit. The application, the toolkit itself
can provide the layer to render the Options and handle callbacks.
Oyranos might provide some of such very commonly used layers. Possibly
this needs to be done as a project outside of Oyranos. Still it will be
a key feature of Oyranos.

The settings, modified or not in the options object will affect the
colour conversion regardless of what level in the process chain. For
instance it is almost the same to create a default Oyranos colour
conversion on system level as on application level. Flags can be
provided to differ for instance for proofing options, as they are only
of interesst on a application level.

### Splitting colorimetry

Here should stay or link to something about the newer 3 part colour
profiles approach in opposite to the ICC's approach.

### Splitting CMMs

[a suggestion brought up by Graeme Gill in a discussion on the xorg
mailing
list](http://lists.freedesktop.org/archives/xorg/2008-March/033531.html)

A CMM does usually provide two basic functions:

-   accept input of several ICC profiles and precalculate the input to
    output colour transformation, usually as n-dimensional tables
-   apply the colour conversion from the input to the output colours
    through the above precalculated table

CMM's might not follow the ICC standard in storing the precalculated
tables. Thus typical a CMM has the possibility to provide a private data
structure to the CMM framework for storing and obtaining it back for
pixel conversion.

-   pro
    -   the CMM can store in a optimised manner its data
-   con
    -   the data is special to one CMM only and can not be exchanged

A CMM framework can require a CMM to store its precalculated tables to a
ICC device link profile and load it on request. This allowes
interessting combinations. For instance it is possible to have a full
fledged CMM, which adhers maturely to the ICC profile standard. An other
CMM migh be reluctant to implement the many required details of the ICC
standard but specialises on a fast colour conversion path. Both can be
easily combined through the ICC conform device link profile, each
bringing in its strength to form a more powerful or greatly adapted CMM.
The pixel conversion specialised CMM has then only to understand the ICC
device link syntax.

-   pro
    -   CMMs can combine functionality
    -   on disk cache with serialised data possible
-   con
    -   time consuming
    -   might be not feature complete

CMM frameworks might even decide to register two allow registering and
controling two types of CMM's according to the two basic functions
outlined above.

-   pro
    -   the CMM can be selected independently
    -   more influence to experiment with the process
    -   better analysing
-   con
    -   more administration and possibly confusion
    -   the same can be reached to provide in the pixel CMM a option to
        select a linking CMM

Late and Early colour binding
-----------------------------

Colour binding means that step in colour workflow where image colours
are turned into a final state. For instance for displaying colours on a
monitor, it is that state when window colours are matched to the
monitors colour space.

The glue between both concepts, which almost always should be available
in parallel, is a explicite opt out flag and a path for colour profiles
to characterise the image data.

![](CMS_Linux2-3.2.png "CMS_Linux2-3.2.png")

### Late colour binding

In the above mentioned context late colour binding means to do the final
colour conversion at a late state. This can have advantages, when colour
needs to be processed later on. Then colours can stay in a well behaved
editing space and processing such as mixing is much more relyable. The
colours should be converted to a device space when no further colour
processing is done. This happens typical on a system level and can be
influenced by a user through system level options.

-   pro (for a xorg example)
    -   twm, xterm .. get colour managed as soon as a composite manager
        is used
    -   many parts need no changes to work
    -   highest consistency possible
-   con (for xorg example)
    -   without any optimisation it can be resource hungry in terms of
        memory and CPU/GPU time
    -   higher bit depth paths might not be available
    -   independend non touching colour path entries can make this
        concept harder to implement (OpenGL, X11, XV, overlay,...)

### Early colour binding

In the above mentioned context early colour binding means to do the
final colour conversion at a early state. This can have advantages, when
colour conversion needs to be controlled as much as possible. It is
possible to display native colours to measure the bahaviour of the
output device. Or colours can be prematched for proofing with otherwise
unusual rendering intents like the absolute colorimetric intent. The
decission about the performed colour transforms are typical made in the
application.

-   pro
    -   most control over options
    -   private conversions or null conversion
    -   can reduce data early to save system data bandwidht
    -   16-bit and HDR data are full available on application level
-   con
    -   speed depends on the CMM
    -   might process more data than nesessary

### Combing early and late binding

A combination of early and late binding can be achived by attaching
during a early state a precalculated device link profile to image data
and process the image data by the provided device link with out external
options be involved.

-   pro
    -   high level options are available (early binding)
    -   low level optimisations can apply at a late state (near
        hardware) (late binding)
-   con
    -   lesser control over the pixel converting CMM selection (late
        binding)
    -   process possibly on low 8-bit data only (late binding)

Flat color vs. mixed mode documents
-----------------------------------

One concept of the ICC-standard, is the possibility to create documents,
where every object (image, vector graphics, text-objects) can have is
own profile and rendering intent. This makes color management of
complete documents very complex and can easily results to unwanted color
transformations of individual objects of an document.

To give users successful experiences with color management, it is useful
to have the option of an color management policy, which allows only the
creation of flat color documents in well known and tested editing
spaces.

![](CMS_Linux2-3.1.png "CMS_Linux2-3.1.png")

Stages of manipulation
----------------------

Handling of colour data is been expected in several states, handled by
dedicated colour spaces. The following describes a process with three
steps for image data.

-   characterise data (tagged with profile or machine readable
    description), unknown or uncertain data -&gt; assign a assumed
    source profile (distinguish Rgb/Cmyk/Gray)
-   editing colour space to tweak, manipulate and blend, mostly with
    enough colour volume
-   output or proofing colour space, considered as a destination for the
    final content. This colour space can be used to check against,
    during editing and possibly convert as the last stage of editing.

Untagged data
-------------

Most difficult is here the mixed behaviour of applications regarding
tagging versus non tagging of exchange data with colour profiles.

### Assign an profile into untagged data

A simple example is a photographer, which is aware of tagging images
correctly and delivers them to his customer. Next step is to include
such tagged photo into an document in an CM unaware word processor by a
different person. The output from the word processor is prepared as pdf
for the web and as pdf for printing. As the word processor is ignoring
any colour profiles, it is up to the system to follow a rule, which
makes the colour data unambiguous.

-   leave it as is for viewing, and interpret as follows below
    -   pros:
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
    used up to date by CM unaware applications
-   differentiate between input path for colour data:
    -   WWW sites -&gt; sRGB
    -   Files from outside of the computer -&gt; selectable profile
    -   Files from inside the computer -&gt; selectable profile

As the source of images, whether they come from out- or inside the
computer, becomes more and more fuzzy, this concept is difficult to
implement.

-   programs use the platform specific colour space
-   cross platform toolkits should specify a policy, to which standard
    they adhere, most useful would be sRGB

### Save onto an untaggable image format

-   warn user about losing colour space information during saving
-   warn on export especially about a colour space different than the
    assumed one

Settings
--------

### Policies

#### Average User

Most people belong to the [Office User
type](/wiki/What_the_users_want#Office_Users_.2F_Webdesigners "wikilink").
They need an reliable conversion behaviour. Simplicity is the main goal
there. [sRGB](/wiki/Standards "wikilink") serves this behaviour well. Defaults
should be set to:

-   assumed RGB - sRGB
-   editing colour space: sRGB
-   convert always data to editing space (before a save, not nice, but
    the most reliable in mixed CM aware environments, this was
    repeatedly criticised)
-   don't prefer mixed colour space documents (keep it simple)

#### Graphics Distribution

[Graphic Designers](/wiki/What_the_users_want#Graphic_Designers "wikilink")
and other specialist may want to use own settings. Here some defaults:

-   assumed RGB - sRGB or Adobe(?)
-   no pop-up for untagged images
-   editing RGB - Adobe,ECI or L-Star (large gamut)
-   convert RGB data during editing to editing space (don't pop up
    dialogs)
-   no pop-up for conversion
-   don't convert CMYK data (because of possibly failed black preserving
    capabilities)
-   allow mixed colour space documents (warning for internet PDF's?)

### Device Settings

The device to device colour path contains as well the settings to
receive and to output colours. This makes the storage of these settings
necessary for a working colour management. Currently such settings are
spread over various places. They are partially stored in application and
OS databases or only partially embedded in profiles, like the vcgt tag.
There should be a format developed and used, which makes it easy to
combine both colour and settings characterisation.

[Device Settings](/wiki/Device_Settings "wikilink")

### Elektra namespace

The idea is to comply to Elektra naming schemes and be extensible to
other data bases too like XML files or possibly the JSON format
suggested by Graeme.

Elektra keys are ordered like paths, and thus separated by a slash. The
top level entry is something like “sw” for application specific things.
In order to get colour stuff recognised, I would suggest to use a top
level category “shared” for system wide colour management settings in
Elektra. Elektra has even a layer above to feature a user/system
distinction, but it shall not matter here. This is the Elektra specific
part. In Oyranos I call this the top part of a configuration path.

*Top:* the top section for the Elektra data base; e.g.

`             `“`share`”  
`             `“`sw`”

The following generic part is to create paths and keys based on the
following arrangement. Each element has to be appended:

*Domain:* a hint about the standard the keys adhere to; e.g.

`             `“`freedesktop.org`”` for shared and specified keys`  
`             `“`oyranos.org`”` for specific things`

*Type:* tell about a classification; e.g.

`             `“`colour`”` for default colour settings and `“`colour_icc`”` for ICC CMM specific keys`  
`             `“`colour_icc`”` for a ICC colour conversion CMM`

Possible is “colour” for a colour transformation workflow, “colour\_icc”
for a ICC CMM, “tonemap” for HDR to LDR mapping, “image” for image
handling, “generic” miscellaneous. Other words should be possible too
but are probably outside of Oyranos' understanding.

*Application:* a real application or a group for standard settings; e.g.

`             `“`profile`”  
`             `“`lcms`”

*Option:* the actual value; e.g.

`             `“`editing_xyz`”  
`             `“`preserve_black`”

**Examples:**

This would lead to the following path + key: a default Rgb editing
space:

`  `“`share/freedesktop.org/colour/profile/editing_rgb`”

for a plug-in or application setting:

`  `“`sw/oyranos.org/colour_icc/lcms/preserve_black`”

The actual value is then to be associated to the key. Which keys shall
be visible to backends? The “Type” level seems the most easy one to
handle that. The option would be passed to the CMM.

`  `“`share/freedesktop.org/colour_icc/behaviour/rendering_intent`”

How split into **advanced** and basic settings? Add a **advanced**
keyword to the Option level (last level) after a point. The point workes
here slightly like a XML attribute. Basic is the default and maps to
zero, so it should not be specified in the option level. In the
following example the key would not be visible to a CMM. The behaviour
is to be matched on a higher level.

`  `“`share/freedesktop.org/colour/behaviour/proof_soft.`**`advanced`**”

User Interface
--------------

### Profile Selection

-   use a flat directory to store all files
    -   easy to read by all applications
    -   needs several mechanisms to distinguish profiles for devices,
        editing ...
-   use directories hierarchically
    -   allow all kind of distinguishing even if not supported by
        Oyranos, other may use nevertheless
    -   easy grouping of device, editing ... profiles
    -   needs a layout and specification

### Common Gui elements

-   [Colour management
    Icon](http://www.freedesktop.org/wiki/OpenIcc/Icons)

Profile selectors can to a user present the internal stored name and the
external file name. Ideally both should coincide, with the possible
exceptions of the space sign and the file type ending. In case the
profile is a in memory one the internal name might not be detectable.

### XML Plug-in options

Simple Toolkit Abstraction is the name of a project idea on the GSoC2008
OpenICC page. Its goal is to provide a simple way for plug-ins and CMM's
to describe options and have some slightly control over its presentation
layout. Jon A. Cruz gave some helpful suggestions on what to focus on
this area. The dataflow could be something like this:

`XFORMS + XML -> xslt -> toolkit XML -> native toolkit widgets`

Requirements:

-   based on W3C technology (Xforms, Dom ...)
-   callback mechanism (possibly to pass the changed serialised widget
    layout, like a diff, to the callback)
-   callback as C function or CTL for portability?
-   easy separation of layout (widgets) from data (options)
-   widget set: tabs, groups, lists, choice list, sliders, buttons,
    check button, radio button, text box, drawing area
-   define orientation (horizontal/vertical for grouping inside a pack
    style widget)
-   select one widget per group for scaling; place this widget at top,
    bottom, right, left, centered or to fill as specified
-   serialise and deserialise from and to XML
-   support console applications
-   converters for at least Qt, Gtk, FLTK ...

Some links to explore:

-   [XML Schema](http://www.w3.org/TR/xmlschema-2/#built-in-datatypes)
    to get a grip on data inside XML
-   [“Useful
    Datatypes”](http://xformsinstitute.com/essentials/browse/book.php#ch04-6-fm2xml)
    @ xformsinstitute
-   [rendering of XFORMS inside
    Mozilla](http://developer.mozilla.org/en/docs/XForms)
-   [Xslt](http://en.wikipedia.org/wiki/Xslt) @ wikipedia
-   [Simple Toolkit
    Abstraction](http://www.freedesktop.org/wiki/OpenIccForGoogleSoC2008#head-07e05f69f1b4e331ba0d3741dc06ba53ae728459)
    OpenICC GSoC2008 project idea

<!-- -->

-   read in [XML Plug-in options](/wiki/XML_Plug-in_options "wikilink") for
    more details

Manipulation
------------

The goal of using manipulations is to get an good image correction for
special cameras, media or special scenes. The process is as well known
in the film industry as colour grading.

Manipulations exist as profiles of ICC type abstract profiles. They are
use by CinePaint or Photoshop for instance. On OS X they are part of the
color management system ColorSync. Therefore I would think at least the
ICC profile version could be included in Oyranos.

Curves today used by CinePaint, Gimp and UFRaw are originally
proprierity ones delivered with Nikon and other software. People
translated them to use in these programs. The format is basically a
response curve telling which intensities should come out for an given
value. These curve files can contain single curves or curves for
multiple channels, like Value, R,G,B, Alpha + ?

Not shure for the curves. Maybe they can be converted to abstract
profiles. Gutenprint handles an own curves format for print settings. It
is XML-based and Robert Krawitz calls them piecewise curves.

One interesting aspect of the Gutenprint XML curves is that they are
editable. For profile editors an approximation algorithm is needed. An
edited profile can be more easily written as CLUT but would probably
loose precision during conversion from an matrix based one.
