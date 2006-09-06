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
completely. For instance downloading a printer profile and separating an
image does not enshure the according driver settings are selected
correctly. Even the driver and its version is often not included and not
standardised to access machine readable. To overcome that information
hole, Apple introduced the vcgt tag to describe the according hardware
state in the graphics card gamma table. This is a single step and maybe
enough for just this task.

In the following proposal I will draw scetchy, what I think is needed to
make the task complete, and apply to other areas too.

### Informations Incorporated

-   device settings (as provided, colour relevant ones should be queried
    automatically)
-   driver names and theyre versions to identify validy of components
    used
-   normally changeable driver settings, which must be fixed for usage
    with the ICC profile
-   colour characterisation (a ICC profile belonging to the above
    settings)
-   priority (generic profile - low, self calibrated - high)

### Advantages

-   select an profile and the system knows about needed settings
-   change settings and the system can tell if an profile is available
-   email a complete settings file, no further information is needed to
    setup
-   use the same settings in all applications, they are globally
    available through the profiles themselves

### Scenario

(X example, similiar to print, scan, digicams):

-   obtain monitor settings informations
-   set/reset monitor settings from software (xcalib/ddccontrol,...)
-   interface to get/set settings from Oyranos to drivers
-   extract ICC information easily
-   allert for expired configuration

### Implementation Details

-   easy accessible text format to store and handle driver informations
    (key/value pairs)
-   driver identifier (which every application can eighter understand or
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
        -   forces a switch first
-   the driver version should be editable (ICC Examin?), so a older
    drivers can be still used

### Oyranos API suggestion

`/** The following function includes all information to create and return the device `  
`    settings tag */`  
`void* oyIccDeviceSettingsDataWrite            ( const char* device_manufacturer, // used for the 'dmnd' tag`  
`                                                const char* device_name,         // used for the 'dmdd' tag`  
`                                                const char* device_serial,`  
`                                                const char* driver_name,`  
`                                                const char* driver_version,`  
`                                                const char* driver_signature,`  
`                                                struct tm*  calibration_time,    // used for the 'calt' tag`  
`                                                                                 // needs <time.h>`  
`                                                void*       configuration_data_block,`  
`                                                size_t      config_block_size,`  
`                                                size_t*     data_size )`  
`return: the device settings data (technically it may be a profile containing the necessary tags)`

`/** a function to allow embedding into a existing profile , possibly including some `  
`    checking of missing other tags like 'calt' - calibrationDateTimeTag */`  
`void* oyIccDeviceSettingsDataEmbedd           ( void*       device_data, // as provided by`  
`                                                                         // oyIccDeviceSettingsDataWrite`  
`                                                size_t      device_data_size,`  
`                                                void*       old_profile,`  
`                                                size_t      old_profile_size,`  
`                                                size_t*     new_profile_size )`  
`return: the new profile`

`/** a function to extract the device settings tag from a existing profile */`  
`oyDeviceSettings_s* oyIccDeviceSettingsDataGet( void*       profile,`  
`                                                size_t      profile_size,`  
`                                                size_t*     data_size )`  
`The oyDeviceSettings_s structure is not yet finished.`

TODO: proof the available options (ICC, XML...), choose, publish a
[specification v0.2](/wiki/Device_Settings_in_ICC_0.2 "wikilink")
([0.1](/wiki/Device_Settings_in_ICC_0.1 "wikilink")) and procedure suggestion,
implement in [Oyranos](/wiki/Oyranos "wikilink")
