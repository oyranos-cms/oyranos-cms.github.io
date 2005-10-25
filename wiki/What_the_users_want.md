---
title: What the users want
permalink: wiki/What_the_users_want/
layout: wiki
---

Note: This page has been vandaliced by spamers in removing content and
placing inadequate messages. Due to this the page is no longer editable
until we find an appropriate solution.

Before we talk about colormanagement policies for applications, we
should think about, what different users expect from colormanagement.

Office Users / Webdesigners
---------------------------

Such users want an easy colormanagement. They don´t want to see pop-up
dialogues, that the profile of an actual file is not fitting to the
colorsettings of their application. RGB-colors should be unambigous
specified by numbers. Input, Monitor, print-output should colormatch.

Graphic Designers
-----------------

They want an easy workflow form delivered RGB-data to a CMYK-Editing
space, which represents a standard printing condition (e.G. SWOP or
ISOcoated). CMYK-colors should be unambigous specified by numbers. The
monitor should simulate the editing CMYK-Editing space. The printout
should also simulate the editing CMYK workingspace and should serve as
proof for the printinghouse. It should be easy to create PDF/X-1a data,
whith the CMYK-Editing space embedded as outputintent.

` Question: should it here read `“`embedded`` ``as`` ``output`` ``profile`”` instead of `“`outputintent`”`?`  
` The rendering intent is a separate option and for Cmyk anyway not applicable, because`  
` an further colour transformation is unlikely. But for interpreatation the profile is needed.`  
` Answer from jphomann: There is a big difference between Output Intent in PDF/X- and`  
` Rendering Intents in ICC-Transformation. The OutputIntent in PDF/X is a ICC-profile or`  
` ASCII Text, which decsribes the colorspace of CMYK-objects in the PDF/X-File, which has`  
` no embedded profiles. (also called DeviceCMYK. This construct is choosen by the ISO TC130,`  
` because CMYK-objects with embedded profiles (also called ICCbasedCMYK) can cause unwanted`  
` colortransformations of this objects during the RIP-process of the PDF-file. `  
` The construct of the output-intent in PDF/X prevents such unwanted colortransformtions.`  
` But the reciever can clearly see, for which CMYK colorspace the PDF/X file was generated.`

They dont like pop-up dialogues, that the profile of an actual file is
not fitting to the colorsettings of their application. They hate
unwanted colortransformtions of CMYK-data, where e.g. black or grey
objects turns to 4-color objects.

` Hint: littleCMS has a black preserving feature with vesion 1.15. About others I dont know.`  
` Answer jphomann: One point is the possibility of the littleCMS. But the applications, which`  
` uses littleCMS must explizit use this feature, which is going ahead normal ICC-wokflows.`

Prepress specialists
--------------------

They do more or less the same like the graphic designers, but want the
most flexible control over the colormanagement-workflow. They need
pop-up dialogues, that the profile of an actual file is not fitting to
the colorsettings of their application. They must deal with different
CMYK-Editing spaces and need control over gamutmapping strategies.

photographers
-------------

They want to use the full gamut of their camera and their inkjet
printers. Editing of pictures should be done in a workingspace, where
equal RGB-numbers result to gray.
