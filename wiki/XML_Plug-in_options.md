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

XForms and HTML elements need to be supported fo the UI definition. The
idea is to have as less layout code there as possible and let the UI
engine decide how to display. The plug-ins should be able to expose the
grouping of their options, their type and icons, labels and so on. To
automate processing, the standard options need to be specified on
Oyranos side.

What is all involved?

-   user categories (filter categories ...)
-   registration strings which can map to paths
    -   e.g. “colour/oyranos.org/colour/lcms/preserve\_black”
-   Oyranos backend API's mapping (CMM need images, profiles and
    options, filters want images + options?)
    -   For backends common dynamic resources should be handled
        elsewhere. Would'nt it be useful to register through a
        specialised module key word handlers? The key words can then be
        used to place specific resources into the UI.
-   UI backend deploy xslt conversions to their xml UI representation
-   event exchange

Requirements
------------

-   based on W3C technology (Xforms, Dom ...)
-   ajax based technology ((X)HTML, CSS and Javascript)

[`KaiUweBehrmann`](/wiki/User%3AKaiUweBehrmann "wikilink")`: does not think it is a good idea to bring too many dependencies into the plug-in system. `

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

