---
title: Concepts
permalink: wiki/Concepts/
layout: wiki
---

**Concepts** which shall help ensuring interoperatibility, ease of
interaction or met other goals. They should serve the end to end
expectations of users. Pros and Cons can be discussed here.

### Diversity

To bring various users and producers together the
ICC[1](http://www.color.org) standard was created. This standard covers
a data format to exchange colour information of devices.

### Precision

The OpenEXR CTL[2](http://www.openexr.com/documentation.html) approach
to use direct colour formulas in GPU shader programs is an try to
increase precision and speed related to the demands of the film
industry.

### Consistency

Editing spaces are a very valuable concept to achive good results during
compositing and manipulating images.

-   colour channels should by equally editing the exposure, behave
    equally regarding saturation (no turning of gray into green)

### Flatcolor vs. mixed mode documents

One concept of the ICC-standard, is the possibility to create documents,
where every object (image, vectorgraphics, text-objects) can have is own
profile and rendering intent. This makes colormanagement of complete
documents very complex and can easily results to unwanted
colortransformations of individual objects of an document. To give users
succesful experiences with colormanagement, it is useful to have the
option of an colormanagement policy, which allows only the creation of
flatcolor documents in well known and tested editing spaces.
