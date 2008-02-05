---
title: Argyll Chart Definition HOWTO
permalink: wiki/Argyll_Chart_Definition_HOWTO/
layout: wiki
---

A brief HOWTO on the creation of Argyll chart definition files (`.cht`).

All descriptions here are based on the [Wolf Faust's “C1”
target](http://www.targets.coloraid.de/). All descriptions are outlined
for a Linux system, but should otherwise apply well for other systems as
well after making some obvious changes.

The [full description of the chart file
definition](http://www.argyllcms.com/doc/cht_format.html) can be found
in the Argyll documentation. However, this entry is meant as a recipe to
create a proper chart file from an arbitrary target. For a closer
description of the fields in the `BOXES` section refer to the original
Argyll documentation.

-   Obtain a good image of chart with scanner or camera (TIFF, no JPEG
    compression, no alpha channel)
-   Create a basic chart file sleleton using `scanin -g`

`$ scanin -g myScan.tif myTarget.cht`

-   When editing, keep a blank line after each section

The skeleton chart file we have obtained through this is in pixel units
for all coordinate values given. Actually it can be done in *any*
values. The `scanin` program goes and uses only the relative proportions
of this file to apply them later to the acquired images of the test
charts. All further coordinates mentioned therefore here are based on
the generated skeleton in pixels.

Now, we need to edit/add the necessary sections for the chart file:

-   **`REF_ROTATION`** -- Keep this section tag with its value, as it is
    necessary to correct some of the values used in the definition for
    rotation angles
-   **`XLIST`** and **`YLIST`** -- Clean up all entries to the
    following:
    -   All corners of diagram
    -   Fiducial marks
    -   All lines used in patch grid marks
    -   Adjust the integer after the `XLIST` and `YLIST` tags to reflect
        the number of entries following in that section
-   **`BOXES`** -- Add this section between the `REF_ROTATION` and the
    `XLIST` sections
    -   Tweak the integer after the `BOXES` tag until it fits (for me
        number of patches + 1 worked, but others are seen in other chart
        files ...)
    -   **F** -- fiducial marks  
        (use top left, top right, and bottom right mark positions)
    -   **D** -- diagnostic box  
        (enclosing the whole “interesting” area of the chart, with
        measuring area and fiducial marks)
    -   **Y** -- sequence boxes, array of patches  
        (columns, then lines)
        -   Coordinates in sequence boxes:
            -   first the range of column labels  
                (start to end, e. g. “`01 22`” for columns 1 through 22)
            -   then the range of line labels  
                (start to end, e. g. “`A L`” for lines “A” through “L”)
            -   width and height of the patch sizes of these sequence
                boxes  
                (e. g. “`36.8 36.8`” for square patches with 36.8 pixel
                units in average size)
            -   top left starting coordinates of the first patch in
                sequence
            -   offset horizontally/vertically of next patches  
                (if the patches are square with no gap next to each
                other this should be the same as the width/height pair
                for the patch size mentioned above)
    -   **X** -- sequence boxes, array of patches (lines, then columns)
        -   Definition the same way as the sequence box above. If the
            box contains a linear array (patches in one straight line
            only), the not needed dimension can be “dummied away” using
            the underscore (“\_”) as a place holder for the label range.
-   **`BOX_SHRINK`** -- “Shrinkage” of patch area (estimate something
    that's sensible in the coordinate units, e. g. 4.0 pixels)
    -   Add this section right after the `BOX_SHRINK` section, still
        before the `XLIST` section
-   **`EXPECTED XYZ`** -- Add measurement values from vendor information
    (e. g. in XYZ colour space). In case of CIE LAB values, replace the
    “`XYZ`” by “`LAB`”.
    -   Add an integer declaring the number of defined measurement
        patches to follow in this section.
    -   Add for each patch the index with the three colour coordinates.
        These can be obtained either through direct measurement with a
        spectrophotometer or from the manufacturer's target specs that
        are usually supplied along with the target. Pad the numbers (if
        necessary) to give “nice” labelling (e. g. `A1` --&gt; `A01`)

`  A01         2.90    2.51    2.30`

Test the created chart description using `scanin` with the used target
image and description creating a diagnostic image with the boxed drawn
in:

`$ scanin -o -dionap myScan.tif myTarget.cht diag.tif`

The image `diag.tif` can be viewed with any image viewer. It should
present all properly aligned and identified patches of the target.
