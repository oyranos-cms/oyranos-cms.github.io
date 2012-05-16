---
title: LibCmpx
permalink: wiki/LibCmpx/
layout: wiki
---

The ***Color-Managed Printing eXtension (libCmpx)*** is a library that
will add color management support to print dialogs.

Architecture
------------

![](Libcmpxmodel_sm.png "Libcmpxmodel_sm.png")

LibCmpx is organized using five distinct components:

**libCmpx API**: The primary interface for an application. It contains
the essential functions for the programmer to initialize
color-management from within the application's print dialog.

For printer color-management to work, the dialog programmer must pass
into libCmpx two sets of input:

-The printer settings as obtained by the dialog (“Print Resolution”,
“Media Type”, “Print Quality”, etc.).

-A PDF file of the ready-to-print image.

The appropriate API calls are shown below in “API Usage”. A libCmpx
Color Management Object struct (*libcmpx\_cm\_t*) is required throughout
the application to pass-in and receive information via libCmpx.

**libCmpx Color Management Layer**: This component is responsible for
delegating the appropriate API calls into the appropriate processing
module(s). What the layer does is execute the algorithms that handle the
library's color-management functionality – data received from a
*libcmpx\_cm\_t* struct is passed either to the “Renderer” or “Selector”
modules (or both, depending on the requested API operation).

**libCmpx Processing Modules**: There are two distinct modules in
libCmpx: **libCmpx Selector** and **libCmpx Renderer**. Both modules are
the heart of libCmpx - the former handling automatic profile-selection
and printer driver calibration, and the latter handling the rendering of
a PDF OutputIntent.

The Selector module uses Oyranos for profile calibration which, through
the use of its CUPS module, handles generating a calibrated PPD file. It
processes the printer settings specified by the user in the print
dialog, and returns back an updated set of options. For instance, if a
user chooses sets an “auto-select ICC profile” mode from the print
dialog, the Selector module will simply return a correct ICC profile
back into a dialog. But if a user instead manually chooses a specific
profile in the dialog, the Selector module will return back calibrated
printer settings.

The Renderer module uses Ghostscript to embed an ICC profile into an
application's output image file, which will then be ready for the print
chain.

**libCmpx Internal**: All of the lower-level operations, structures, and
definitions required from the processing modules are stored in libCmpx
internal.

Dependencies
------------

The library depends on Oyranos for profile selection, as well as
Ghostscript to render the PDF. In addition, CUPS is required to handle
PPD files.

Version requirements for these dependencies are as follows:

-   Oyranos (the up-to-date [git
    version](http://www.oyranos.org/wiki/index.php?title=Oyranos/git))
-   [Ghostscript](http://pages.cs.wisc.edu/~ghost/) (9.04)
-   [CUPS](http://www.cups.org/software.php) (1.5.0)

Installation
------------

libCmpx can be obtained through git.

`$ git clone `[`git://gitorious.org/libcmpx/libcmpx.git`](git://gitorious.org/libcmpx/libcmpx.git)

Once the project is downloaded, enter its root directory and type the
following:

`$ mkdir build`  
`$ cd build`  
`$ cmake ..`  
`$ make`  
`$ make install`

After installing libcmpx, a test print dialog can be launched using the
following command from any place in your console:

`$ cmpxDiag`

Updates can be obtained by typing:

`$ git pull`

API Usage
---------

The libCmpx API is based on the prototype library invented for the
[XCPD](http://www.oyranos.org/wiki/index.php?title=XCPD#API_Usage). As
such, the API usage is very similar between the two.

##### Sample Code

The following code demonstrates printer profile selection and PDF
rendering using the libCmpx API.

`<libcmpx.h>`

`libcmpx_selectormode_t getProfileSelectionMode();`  
`void setManualProfile(libcmpx_cm_t**);`

`int main()`  
`{`  
`   /* Optional status enums */`  
`   libcmpx_sstatus_t selector_status;`  
`   libcmpx_rstatus_t renderer_status;`  
  
`   /* Initialize API color management */`  
`   libcmpx_cm_t* cm = libcmpxCM_initialize();     `  
  
`   /* Open PPD file. */`  
`   ppd_file_t* ppd = ppdOpenFile(`“`ppdfile.ppd`”`);`  
  
`   /* Get profile selection mode from the GUI. (see box below) */`  
`   libcmpx_selectormode_t mode = getProfileSelectionMode(cm); `  
  
`   /* Set the profile based on the dialog selection */`  
`   if(mode == LIBCMPX_USERSELECT_MODE)`  
`     setManualProfile(&cm);`  
`   else if (mode != LIBCMPX_SELECTORMODE_NOTSET)`  
`     selector_status = libcmpxCM_setProfileFromPPD(&cm, &ppd, mode);`  
  
`   /* Render the PDF */`  
`   renderer_status = libcmpxCM_setSpoolPdf(&cm, 0);`  
  
`   libcmpxCM_close(&cm);`  
  
`   return 0;`  
`}`

The following helper functions are part of the ICC profile selection in
the UI. (Using Qt.)

`QString iccModeString;`  
`QComboBox iccModeComboBox;`

`libcmpx_selectormode_t getProfileSelectionMode()`  
`{`  
`  iccModeString = iccModeComboBox.currentText(); `  
  
`  if(iccModeString == `“`Auto`` ``Set`”`)`  
`   return LIBCMPX_AUTOSELECT_MODE;`  
`  else if (iccModeString == `“`Application`` ``Set`”`)`  
`   return LIBCMPX_SYSTEMSELECT_MODE;`  
`  else if (iccModeString == `“`Manual`”`) `  
`   return LIBCMPX_USERSELECT_MODE; `  
`  else`  
`   return LIBCMPX_SELECTORMODE_NOTSET;`  
`}`  
  
`void setManualProfile(libcmpx_cm_t** cm_obj)`  
`{`  
`   QString userSelection = QFileDialog::getOpenFileName(. . .);`  
`   const char* user_profile = userSelection.toLocal8Bit();`  
  
`   libcmpxCM_setProfile(cm_obj, user_profile);  `  
`}`
