---
title: XCPD
permalink: wiki/XCPD/
layout: wiki
---

The ***eXperimental Common Printing Dialog (XCPD)*** is an application
that was developed during the 2011 Google Summer of Code. Its goal is to
provide a model that adds color management to the CPD.

Project Overview
----------------

API Usage
---------

The following sections demonstrate how the XCPD library API works.

##### Initialization

An *XCPD Color Manager* object is used throughout the XCPD as the
driving mechanism for color management. It is initialized by way of the
following:

`xcpd_cm_t* cm_obj = xcpdCM_initialize();`

To de-allocate a Color Manager object, simply use the “close” function:

`xcpdCM_close(cm_obj);`

##### Profile Selection

Profile selection is handled via Oyranos. Its job is to receive
configuration data from a PPD file -- specifically during the the
selection of printer options by the user -- and apply the
profile-selection workflow described in [Device
Settings](http://www.oyranos.org/wiki/index.php?title=Device_Settings#Profile_Selection).

A function named **xcpdCM\_setProfileFromPPD()** is to be called in
order to initiate the profile-selection sequence. A ppd\_file\_t\*
object must be marked with the user-selected options prior to sending it
into this function, along with an xcpd\_cm\_t\* object. What is returned
is both the xcpd\_cm\_t\* object with an appropriate profile, and a
xcpdcm\_sstatus\_t result enumeration.

`/* Initialize XCPD CM object and load a PPD file */`  
`xcpd_cm_t* cm_obj = xcpdCM_initialize();`  
`ppd_file_t* ppd = ppdOpenFile(`“`ppdfile.ppd`”`);`

`/* Select dialog options by marking the PPD file object.*/`  
`xcpdcm_sstatus_t result = xcpdCM_setProfileFromPPD(cm_obj,ppd);`

`/* Use the returned xcpdcm_sstatus_t enum to check for success */`  
`if(result != XCPDCM_SELECTOR_INVALID_PPD || result != XCPDCM_SELECTOR_NOPROFILE)`  
`  puts(xcpdCM_getProfile(cm_obj));`

###### Alternate Usage

In the case where a static PPD file does not have options to read in ICC
profile mode selection, the XCPD CM API provides an explicit solution
that uses **xcpdCM\_setProfileFromPPD2()**.

This function requires an additional xcpdcm\_selectormode\_t enum
parameter, which will have been set each time a user selects an ICC
selection option directly from the UI.

`QString iccModeString;`  
`QComboBox iccModeComboBox;`

`/* Set up Color Manager object and XCPD selector mode enumeration. */`  
`xcpd_cm_t* cm_obj = xcpdCM_initialize();`  
`xcpdcm_selectormode_t mode;`

`/* Open PPD file*/`  
`ppd_file_t* ppd = ppdOpenFile(`“`ppdfile.ppd`”`);`

`/* The following is code for ICC profile selection segment in the UI. */`  
`iccModeString = iccModeComboBox.currentText();`  
`if(iccModeString == `“`Auto`` ``Set`”`)`  
` mode = XCPDCM_AUTOSELECT_MODE;`  
`else if (iccModeString == `“`Application`` ``Set`”`)`  
` mode = XCPDCM_SYSTEMSELECT_MODE;`  
`// In this case, we must explicitly set a profile into XCPDCM.`  
`else if (iccModeString == `“`Manual`”`) {`  
` mode = XCPDCM_USERSELECT_MODE; `  
` QString userSelection = QFileDialog::getOpenFileName( ... );`  
` const char* user_profile = userSelection.toLocal8Bit();`  
` xcpdCM_setProfile(user_profile, cm_obj);  `  
`}`

`/* The last segment of the code will call a refresh`  
`of the profile settings based on ICC mode...*/`  
`xcpdcm_sstatus_result = xcpdCM_setProfileFromPPD2(cm_obj, ppd, mode);`

##### PDF Rendering

XCPD library API is able render a spool-ready PDF file by way of a call
to the **xcpdCM\_setSpoolPdf()** function. It is required that the XCPD
Color Manager object contain a PDF file set prior to using this.

`/* Load a PDF file into the XCPD Color Manager object */`  
`int error = xcpdCM_setPdfFile(`“`myPdf.pdf`”`, cm_obj);`

`/* Render the PDF */`  
`xcpdcm_rstatus_t render_status;`  
`render_status = xcpdCM_setSpoolPdf(cm_obj);`
