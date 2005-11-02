---
title: Device Settings
permalink: wiki/Device_Settings/
layout: wiki
---

All variable parts of the colour processing chain must be taken into
account, to achieve predictable results. As a consequence colour
profiles as colour only transformations are not enough to describe
completely. For instance downloading a printer profile and separating an
image does not enshure the according driver settings are selected
correctly. Even the driver and its version is often not included and not
standardised to access machine readable. To overcome that information
hole, Apple introduced the vcgt tag to describe the according hardware
state in the grafics card gamma table. This is a single step and maybe
enough for just this task.

In the following proposal I will draw scetchy, what I think is needed to
make the task complete, and apply to other areas too.

### Informations Incorporated

-   device settings (as provided, colour relevant ones should be queried
    automatically)
-   driver names and theyre versions to identify validy of components
    used
-   changeable driver settings
-   colour characterisation (a ICC profile belonging to the above
    settings)

### Advantages

-   select an profile and the system knows about needed settings
-   change settings and the system can tell if an profile is available
-   email a complete settings file, no further information is needed to
    setup
-   use the same settings in all applications, they are globally
    available

### Scenario

(X example, similiar to print, scan, digicams):

-   obtain monitor settings informations
-   set/reset monitor settings from software (xcalib/ddccontrol,...)
-   interface to get/set settings from Oyranos to drivers
-   extract ICC information easily

### Implementation Details

-   easy accessible text format to store and handle driver informations
    (key/value pairs)
-   combine with ICC profiles
-   add device settings information to an existing ICC profile
    -   use a internal dedicated ICC profile tag
        -   possibly hard to circumvent license issues
        -   best to identify, without breaking ICC standards
        -   allow profilers do handle themself (by an small library)
        -   need possibiliy to add that information after profiling,
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

TODO: proof the available options (ICC, XML...), choose, publish a
specification, implement in [Oyranos](/wiki/Oyranos "wikilink")
