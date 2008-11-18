---
title: XML Plug-in options
permalink: wiki/XML_Plug-in_options/
layout: wiki
tags:
 - Concepts
 - Oyranos
---

Simple Toolkit Abstraction is the name of a project idea on the GSoC2008
OpenICC page. Its goal is to provide a simple way for plug-ins and CMM's
to describe options and have some slightly control over its presentation
layout. Jon A. Cruz gave some helpful suggestions on what to focus on
this area.

Architecture
------------

The dataflow could be something like this:

`XFORMS + XML -> xslt -> toolkit XML -> native toolkit widgets`

XForms and HTML elements need to be supported for the UI definition. The
idea is to have as less layout code there as possible and let the UI
engine decide how to display. The plug-ins should be able to expose the
grouping of their options, their type and icons, labels and so on. To
automate processing, some default options need to be specified on
Oyranos side.

Who is who:

`key handlers (Elektra) <------> XFORMS interpreters`  
`                ^                   ^`  
`                 \                 /`  
`                  v               v`  
`                   plug-in (hooks)`

'''Key Values pairs ''' are stored in Elektra.

**XFORMS interpreters** are selectable libraries to provide widgets or
entire dialog windows for drawing the UI content. They draw XFORMS
documents with toolkit widgets.

**Plug-ins** register not only key, they provide a UI description for
those keys and helpers to handle the key manipulations in a GUI.

What is all involved?

-   key names or registration strings, which map to Elektra paths and
    the XFORMS data model
    -   e.g. “colour/oyranos.org/colour\_icc/lcms/preserve\_black”
        (should be suficient for Elektra)
-   i18n for widget labels and tooltips translation
    -   possibly through gettext or by dynamic XFORMS code generation,
        where this can be done by plug-in code on the fly
-   UI backends (toollkits) deploy xslt conversions to their native xml
    UI representation
-   event handling
    -   plug-in side hook to verify user input
    -   it is unclear to me whether [XFORMS
        evaluation](http://www.w3.org/TR/xforms/#expr-lib) is sufficient
    -   hooks to talk back to plug-in
    -   according UI refreshing
-   UI generation
    -   plug-in side generator of new UI document part
    -   hook to allow for fetching external data (ICC profiles from
        disk, device informations from services, ...)
-   differentiated representations and their conversions:
    -   in memory C struct
    -   permanent disk storage
    -   XML/XFORMS de-/serialisation

<!-- -->

-   Oyranos backend API's mapping (CMM need images, profiles and
    options, filters want images + options?)
    -   For backends common dynamic resources should be handled
        elsewhere. Would'nt it be useful to register through a
        specialised module key word handlers? The key words can then be
        used to place specific resources into the UI.

Requirements
------------

-   based on W3C technology (Xforms, Dom ...)
-   slim XML footprint
-   callback mechanism (possibly to pass the changed serialised widget
    layout, like a diff, to the callback)
-   callback as C function or CTL for portability?
-   easy separation of layout (widgets) from data (options)
    -   should work fairly good with XForms
    -   a form is required on how to present the Oyranos options in
        XFORMS and an easy way to convert between both.
-   widget set: tabs, groups, lists, choice list, sliders (range),
    buttons, check button, radio button, text box, drawing area
    -   there shouldnt be a problem using interactive and
        non-interactive widgets using AJAX technology
    -   screenshots / forms selection
        -   currently I am exploring processors:
        -   [Firefox 2 +
            3](https://addons.mozilla.org/de/firefox/addon/824) 2.0.0.13
            with XForms-v0.8.5 does with a xforms.xhtml (not \*.html)
        -   [Orbeon](http://www.orbeon.com) looks nice but seems rather
            big and needs a local tomcat compilation
-   select one widget per group for scaling; place this widget at top,
    bottom, right, left, centered or to fill as specified
-   serialise and deserialise from Oyranos C struct oyOption\_s to
    XML/XForms and back
-   support console applications
-   converters for at least Qt, Gtk, FLTK ...
-   XML data models will be made by using XML\_Schema (W3C).

References
----------

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
-   [Open Source Java Implementation of the W3C XForms
    standard](http://chiba.sourceforge.net/)
-   [Official XForms site](http://www.w3.org/TR/xforms/)
-   [XFORMS](http://en.wikibooks.org/wiki/XForms) @ wikibooks
-   [XFORMS in
    Firefox](http://www.ibm.com/developerworks/xml/library/x-xformsfirefox/)
    @ ibm

