---
title: Device Settings
permalink: wiki/Device_Settings/
layout: wiki
tags:
 - Concepts
 - Oyranos
---

All variable parts of the colour processing chain must be taken into
account, to achieve predictable results. As a consequence colour
profiles as colour only transformations are not enough to describe
completely the path colours has to go. For instance downloading a
printer profile and separating an image does not ensure the according
driver settings are selected correctly or even the appropriate driver
was used. Even the driver and its version is often not included and not
standardised to access machine readable. To overcome that information
hole for monitors, Apple introduced the vcgt tag to describe the
according hardware state in the graphics card gamma table. This is a
single step and maybe enough for just this task.

In the following proposal, I will draw sketchy, what I think is needed
to make the task complete, and apply to other areas too.

------------------------------------------------------------------------

### Informations Incorporated

-   device identification
    -   device type, manufacturer, model, serial number, country, device
        options

  
  
AB & Co Ltd., printer model CD-1234, EF photo ink, GH gloss paper,
\#1234-5678

-   driver names and their versions to verify integrity

  
nv/nvidia, Gutenprint/HPIJS, DCraw versions

The driver names used must be unique to later lookup and find the
appropriate profile. If one application use Gutenprint and an other
gimp-print chances are high to not find the according profile. Of course
some kind of registering probably with a enumeration type would help
here. With a good maintained database this should work fine.

The driver must be able to tell: down to what driver version he is
colour compatible for a certain device.

-   device settings (as provided, colour relevant ones should be query
    able by a device driver API)

  
expl. PPD, scan parameters, VCGT

-   -   fixing colour sensible driver settings in a GUI to exclude wrong
        user interaction is a precondition to form a calibration

  
  
PPD with removed choices, VCGT + fixed monitor settings, DCraw called
with specified options

-   device colour characterisation (a ICC profile belonging to the above
    outlined calibration)
    -   the profile must belong to the device/driver/settings/version
        mix
    -   priority among selected profiles (generic profile - low, self
        calibrated - high) can be a profile property
    -   fuzzy device/driver settings match [outlined by Graeme
        here](http://lists.freedesktop.org/archives/openicc/2005q2/000313.html)
-   distribute by combining above information
    -   packing all informations into one piece

  
embed into ICC profile, register in a local or remote hardware db, xml
configuration

------------------------------------------------------------------------

### Advantages

-   select an profile and the system/application selects the correct
    driver and knows about needed settings
-   change settings and the system can tell if an profile is available
-   email a complete settings file, no further information is needed to
    setup
-   use the same settings in all applications, they are globally
    available through the profiles themselves

### Scenario

(X example, similar to print, scan, digicams):

-   obtain monitor settings informations
-   set/reset monitor settings from software (xcalib/ddccontrol,...)
-   interface to get/set settings from Oyranos to drivers
-   extract ICC information easily
-   alert for expired configuration

![](Device_profiles_01.png "fig:Device_profiles_01.png")[as Inkscape
SVG](http://www.oyranos.org/wiki/images/d/da/Device_profiles_01.svg)

### Driver

![](Device_profiles_03.png "Device_profiles_03.png")

The big question is, where are driver properties are agreed upon between
two applications. The device part will be handled by Oyranos, thats
clear. The device configuration backends handle especially the device
property to Oyranos DB key mapping. Does it make sense to facilitate a
driver backend API to do the same for various drivers? Logical? No,
devices access and drivers overlap so much, that it is not useful to
split them.

`/* possible sequence to get a device profile - unimplemented */`  
`oyDevice_s * device = 0;`  
`oyProfile_s * profile = 0;`  
  
`oyDeviceGet( `“`config`”`, `“`camera.dcraw`”`, `“`absorber-2.0`”`, 0, &device );`  
`oyDeviceSetDriverContext( device, (void*) driver_context_pointer, (const char*) `“`string.dcraw.xml`”`, (size_t)0 );`  
`oyDeviceGetProfile( device, &profile );`

### Profiling

![](Device_profiles_04.png "Device_profiles_04.png")

### Implementation Details

-   easy accessible text format to store and handle driver informations
    (key/value pairs) in the Oyranos DB

![](Device_profiles_02.png "Device_profiles_02.png")

-   driver identifier (which every application can either understand or
    reject the whole profile)
-   possibly allow data blobs too, to allow compressed content
-   Graeme Gill suggested to use an magic number to identify the blob.
-   additional part within this format to store CMM specific thing
    (expire date, ...)
-   combine with ICC profiles
-   add device settings information to an existing ICC profile
    -   use a internal dedicated ICC profile tag
        -   possibly hard to circumvent license issues
        -   best to identify, without breaking ICC standards
        -   allow profilers do handle themselves (by an small library)
        -   need possibility to add that information after profiling,
            because the device informations may not be available at
            profiling time or the profiler is simply not aware of our
            demand
    -   check and correct the size tag in ICC profiles and append the
        device settings text behind. The profile size would be the
        offset to that data.
        -   profile readers and CMMs would handle as usual
        -   non standard
        -   someone else can use the same approach, which would make
            such data useless
        -   give the modified a proper extension to identify; ?? ICG for
            instance (InterColorprofileGathering) ??
    -   prepend the text and define an offset to the ICC profile data
        -   breaks existing CMMs and profile readers
        -   clear to handle, to be covered by an specification
        -   forces a switch first
-   the driver version should be editable (ICC Examin?), so a older
    drivers can be still used

### Oyranos API suggestion

`/** The following function includes all information to create and return the device `  
`    settings tag */`  
`int           oyProfile_AddDeviceSettings     ( const char* device_manufacturer, // used for the 'dmnd' tag`  
`                                                const char* device_name,         // used for the 'dmdd' tag`  
`                                                const char* device_serial,       // `  
`                                                const char* driver_name,         // just for information`  
`                                                const char* driver_signature,    // to choose the driver`  
`                                                const char* driver_version,      // to choose the driver`  
`                                                struct tm * calibration_time,    // used for the 'calt' tag`  
`                                                                                 // needs <time.h>`  
`                                                void*       configuration_data_block,`  
`                                                size_t      config_block_size,`  
`                                                oyProfile_s* profile,            // profile to embed into )`  
`return: error status`

`/** a function to extract the device settings tag from a existing profile */`  
`oyDeviceSettings_s* oyIccDeviceSettingsDataGet( oyProfile_s* profile,`  
`                                                size_t*     data_size )`

For the oyDeviceSettings\_s structure see the proposal below.

TODO: proof the available options (ICC, XML...), choose, publish a
specification and procedure suggestion, implement in
[Oyranos](/wiki/Oyranos "wikilink")

### Specification

| [Device Settings in ICC](/wiki/Device_Settings "wikilink") Revision History |
|-----------------------------------------------------------------------|
| [v0.1](/wiki/Device_Settings_in_ICC_0.1 "wikilink")                         |
| [v0.2](/wiki/Device_Settings_in_ICC_0.2 "wikilink")                         |
||

TODO (v0.3):

-   The Priority field should be limited to one profiler. Otherwise its
    value is object for concurency, which is not desireable.
-   change the name to 'drvS' to tell its dedication is about driver
    settings not device resolving
    -   remove the device resolving and hint to use the 'pddt' tag
        instead
-   rename the **Device Settings in ICC** to **Driver Settings in ICC**

### Specific Considerations

#### Printing

The proclaimed

`wget `[`http://localhost:631/profiles/sRGB.icc`](http://localhost:631/profiles/sRGB.icc)

is not working in CUPS(v1.2), as pointed out by Hal V. Engel and
[confimed](http://www.cups.org/str.php?L2894) by Mike Sweet.

A path to send a user selected local device profile to a remote print
host is unclear, at least to me.

The limitation of one CUPS profile directory, e.g.
“/usr/share/cups/profiles”, is too restsictive, even with linking to
other directories. The cupsICCProfile attribute should therefore allow
for absolute locations, not just relative to a CUPS profile directory.
The CUPS\_DATADIR seems not a appropriate mechanism.

A print job should reflect the users local settings in regards of
rendering intent selection, editing space and so on. How are profiles,
rendering intents and other settings passed from a printing application
to backends, e.g. the \*toraster family. Do the RPI's need to parse the
PPD in order to read the cupsICCProfile PPD attribute? How copy localy
stored profiles to remote printing hosts?

Linux will [switch to
PDF](http://www.linuxfoundation.org/en/OpenPrinting/PDF_as_Standard_Print_Job_Format)
as standard format for printing. The advantage of Ghostscript would be
to obtain [PDF colour
management](https://www.linuxfoundation.org/en/OpenPrinting/Color_Management)
right from the beginning.

Issues:

-   \[fixed\] [Ghostscript](/wiki/Ghostscript "wikilink") has a [not working
    pdftoraster](http://bugs.ghostscript.com/show_bug.cgi?id=690101)
    filter.

Desireable APIs for Oyranos:

-   obtain a profile by giving Oyranos a static PPD (one without all
    open choices stripped).
-   obtain a list of profile/static\_PPD combinations for a specific
    print queue.

<!-- -->

-   see [Ghostscript](/wiki/Ghostscript "wikilink") to build a test workflow

#### Camera Raw Developing

-   [DNG](http://www.adobe.com/products/dng)

...

### References

-   [Oyranos/X11 Requirements](/wiki/Oyranos/X11_Requirements "wikilink")
-   [PDF colour management wiki
    page](https://www.linuxfoundation.org/en/OpenPrinting/Color_Management)
    @linuxfoundation/OpenPrinting
-   CUPS and ICC colour management
    [email](http://lists.freedesktop.org/archives/openicc/2005q2/000227.html)
    [thread](http://lists.freedesktop.org/archives/openicc/2005q2/000208.html)
    on [OpenICC](/wiki/OpenICC "wikilink")
-   CUPS on [linuxfoundation.org](http://linuxfoundation.org/en/CUPS)
-   v4 ICC support request for Ghostscript [\#688036
    (bugs.ghostscript.com)](http://bugs.ghostscript.com/show_bug.cgi?id=688036)
-   [not working pdftoraster bug \#690101
    (bugs.ghostscript.com)](http://bugs.ghostscript.com/show_bug.cgi?id=690101)
    in Ghostscript
-   Poppler CM request [\#17499
    (bugs.fd.o)](https://bugs.freedesktop.org/show_bug.cgi?id=17499)
-   [OpenPrinting CM
    page](https://www.linuxfoundation.org/en/OpenPrinting/Color_Management)
    @ linuxfoundation

