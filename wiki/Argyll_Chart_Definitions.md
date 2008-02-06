---
title: Argyll Chart Definitions
permalink: wiki/Argyll_Chart_Definitions/
layout: wiki
---

Some contributed Argyll chart definition files (`.cht` files).

-   [Wolf Faust targets](http://www.targets.coloraid.de/):
    -   C1 target (IT8.7/2-1993, 2006:01, batch\# (“Charge”): R060101)
        -   D50 illuminant, 2 deg observer:
            ![](WolfFaustC1_D50_2deg.cht "fig:WolfFaustC1_D50_2deg.cht")
        -   D65 illuminant, 2 deg observer:
            ![](WolfFaustC1_D65_2deg.cht "fig:WolfFaustC1_D65_2deg.cht")
-   [Christophe Métairie
    Photographie](http://www.christophe-metairie-photographie.com)
    -   [DigitaL TargeT
        003](http://pagesperso-orange.fr/christophe.metairie.photographie/eng%20digital%20target.html#The%20DigitaL%20TargeT)
        (produced 2007, batch\# 0349)
        -   D50 illuminant, 2 deg observer:
            ![](DigitalTarget003_D50_2deg.cht "fig:DigitalTarget003_D50_2deg.cht")
        -   D65 illuminant, 2 deg observer:
            ![](DigitalTarget003_D65_2deg.cht "fig:DigitalTarget003_D65_2deg.cht")
-   [X-Rite/GretagMacbeth](http://www.xrite.com/product_overview.aspx?ID=820&Action=Specifications)
    -   [(24 patch)
        ColorChecker](http://www.babelcolor.com/main_level/ColorChecker.htm)
        (March 2007 edition, see note <sup>\[1\]</sup> below)
        -   D50 illuminant, 2 deg observer:
            ![](ColorChecker_D50_2deg.cht "fig:ColorChecker_D50_2deg.cht")
        -   D65 illuminant, 2 deg observer:
            ![](ColorChecker_D65_2deg.cht "fig:ColorChecker_D65_2deg.cht")

<small><sup>\[1\]</sup> **Note:** Vendor information on the ground truth
colour patch data based on X-Rite/GreatagMacbeth data from the
BabelColor web site was used:
<http://www.babelcolor.com/main_level/ColorChecker.htm>

Expected XYZ colour values for the D50/2 deg. observer were computed
from xyY values provided by BabelColor (based on vendor information).

The conversion D50 --&gt; D65 illuminant was performed according to the
pre-computed chromatic adaptation transformation matrix using the
Bradford transformation as provided by Bruce Lindbloom on his web site:
<http://www.brucelindbloom.com/Eqn_ChromAdapt.html> </small>
