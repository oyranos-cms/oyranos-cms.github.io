---
title: OpenICC Configuration 0.1
permalink: wiki/OpenICC_Configuration_0.1/
layout: wiki
tags:
 - Oyranos
 - Standards
---

<h1>
DRAFT

</h1>
| Revision History                                                                                                |
|-----------------------------------------------------------------------------------------------------------------|
| [ucmm](http://lists.freedesktop.org/archives/openicc/2008q2/001615.html)                                        |
| [ICC meta Tag for Monitor Profiles - DRAFT 3](http://lists.freedesktop.org/archives/openicc/2010q4/002293.html) |
| OpenICC Configuration - 1.0 DRAFT 1                                                                             |
| OpenICC Configuration - 1.0 DRAFT 2                                                                             |
||

Introduction
------------

The OpenICC Configuration, in the following text simply named
Configuration, is intended to share common configuration properties
through colour management systems and desktops environments.

Specification
-------------

The Configuration uses the JSON format to store data.

### Format

The Configuration is stored in the well known JSON format inside a tree
data structure. The key prefix contains “org”/“freedesktop”/“openicc”.

Keys are usually grouped into sets either by namespaces like “devices”
or by JSON format arrays.

JSON keys are literal strings in ASCII. Values are literal strings in
UTF-8. It is recommended to write floating point numbers as strings to
avoid imprecision during reading.

### Keys

Keys can have a key prefix to handle key sets like flat data in the ICC
meta tag. A prefix consists of upper case letters \[:alpha:\] and ends
with a underscore '\_'. The key name itself should be lower case and
separated by underscore '\_'. The string for the 'model' key with the
'EDID\_' prefix would become “EDID\_model”.

The “prefix” key is optional and can contain a comma ',' separated list
of prefixes for key names. A interpreter can then easily remove the
prefix to search for common key names in the data base, while
maintaining the origin. “EDID\_model” can be resolved to “model” in
absence of a explicit “model” key. Example “prefix”=“EDID\_,OSD\_”.

“icc\_profile\_hash” optionally contains the ICC hash value to specify a
ICC profile.

“icc\_profile\_file” optionally contains the ICC profiles file name.

“creation\_date” mandatory contains the date and time of entry creation
and should be updated on each change. Something human readable would be
great. But we can as well agree about an other format.

“expire\_date” optionally contains data/time for showing a user a
message to update the profile with a new one.

“automatic\_assignment” mandatory contains “1” for automatic generated
fallback style profiles in a local DB. “0” is to be used for explicit
set user selected profiles. This is useful to know which profiles should
easily be overridden.

Example:

`{`  
`  `“`org`”`: {`  
`    `“`freedesktop`”`: {`  
`      `“`openicc`”`: {`  
`        `“`device`”`: {`  
`          `“`monitor`”`: [`  
`            { `“`prefix`”`: `“`EDID_`”`,`  
`              `“`EDID_model`”`: `“`LCD`` ``one`”`,`  
`              `“`icc_profile_file`”`: `“`profile_name_from_edid.icc`”`,`  
`              `“`creation_date`”`: `“`05-08-11T11:59:50Z`”`,`  
`              `“`expire_date`”`: `“`05-08-12T11:59:50Z`”`,`  
`              `“`automatic_assigment`”`: `“`1`”  
`            },`  
`            { `“`prefix`”`: `“`EDID_`”`,`  
`              `“`EDID_model`”`: `“`LCD`` ``two`”`,`  
`              `“`icc_profile`”`: `“`profile_name_vendor.icc`”`,`  
`              `“`creation_date`”`: `“`05-08-11T11:59:50Z`”`,`  
`              `“`expire_date`”`: `“`05-08-12T11:59:50Z`”`,`  
`              `“`automatic_assigment`”`: `“`0`”  
`            }`  
`          }`  
`        }`  
`      }`  
`    }`  
`  }`  
`}`

### Locations

File locations to write to are:

local: $XDG\_CONFIG\_HOME/color/settings/ or ~/.config/color/settings/

global: /etc/xdg/color/settings/

Read from $XDG\_CONFIG\_DIRS/color/settings/ directory. The
Configuration file ending is 'json'.

The Configuration JSON can be used as file or by a in memory string
representation for exchange among supporting applications.

### Devices DB

The initial key name space is as explained in the Format section
“org”/“freedesktop”/“openicc”. The following name space level is
“device”. Then on of the device classes “camera”, “monitor”, “printer”
or “scanner” is to be used. The devices are stored in a JSON array. Each
entry contains a set of keys and values.

The data base file name is “openicc-devices.json”.

### Defaults DB

The key name space starts as explained in the Format section with
“org”/“freedesktop”/“openicc”. The data base file name is
“openicc-defaults.json”.

References
----------

1. [International Color Consortium](http://www.color.org)

2. [JSON](http://www.json.org)

3. meta tag -
<http://www.color.org/ICCSpecRevision_25-02-10_dictType.pdf>

4. ISO 8601 - Data elements and interchange formats – Information
interchange – Representation of dates and times

2010-2012 © Kai-Uwe Behrmann

[back --&gt; Oyranos](/wiki/Oyranos "wikilink") or [Device
Settings](/wiki/Device_Settings "wikilink")
