---
title: Argyll Chart Definitions
permalink: wiki/Argyll_Chart_Definitions/
layout: wiki
---

Some contributed Argyll chart definition files (`.cht` files).

-   [Wolf Faust targets](http://www.targets.coloraid.de/):
    -   C1 target  
        `it8.cht` file as shipped with ArgyllCMS can be used
-   [Christophe Métairie
    Photographie](http://www.christophe-metairie-photographie.com)
    -   [DigitaL TargeT
        003](http://pagesperso-orange.fr/christophe.metairie.photographie/eng%20digital%20target.html#The%20DigitaL%20TargeT)
        (produced 2007, batch\# 0349)  
        ![](DigitalTarget003.cht "fig:DigitalTarget003.cht")
-   [X-Rite/GretagMacbeth](http://www.xrite.com/product_overview.aspx?ID=820&Action=Specifications)
    -   [(24 patch)
        ColorChecker](http://www.babelcolor.com/main_level/ColorChecker.htm)
        (March 2007 edition, see note <sup>\[1\]</sup> below)  
        ![](ColorChecker.cht "fig:ColorChecker.cht")
    -   CIE colour reference files <sup>\[2\]</sup>
        -   ![](ColorChecker_vendor_D50_2deg.cie "fig:ColorChecker_vendor_D50_2deg.cie")
        -   ![](ColorChecker_vendor_D65_2deg.cie "fig:ColorChecker_vendor_D65_2deg.cie")
        -   ![](ColorChecker_avg_D50_2deg.cie "fig:ColorChecker_avg_D50_2deg.cie")
        -   ![](ColorChecker_avg_D65_2deg.cie "fig:ColorChecker_avg_D65_2deg.cie")

Notes
-----

<sup>\[1\]</sup> Vendor information on the ground truth colour patch
data based on X-Rite/GreatagMacbeth data from the BabelColor web site
was used: <http://www.babelcolor.com/main_level/ColorChecker.htm>

Expected XYZ colour values for the D50/2 deg. observer were computed
from xyY values provided by BabelColor (based on vendor information).

<sup>\[2\]</sup> Vendor's colour information is compiled from data
provided by X-Rite/GreatagMacbeth with the mass produced colour charts.
XYZ values for the files has been computed from the provided CIE LAB
(D50/2deg) values, chromatic adaptation transformations (where necessary
for D65) have been computed using the Bradford transformation.
