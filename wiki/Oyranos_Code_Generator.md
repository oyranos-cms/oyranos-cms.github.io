---
title: Oyranos/Code Generator
permalink: wiki/Oyranos/Code_Generator/
layout: wiki
---

How it works
------------

### Overview

The **oyAPIGenerator** executable takes 3 arguments as input.

-   A directory the templates files using the grantlee format.
-   A source directory with all included code from the templates.
-   An output directory were all auto-generated code is created.

All are optional, and in an *in source* build none of them is actually
used, because they get the default values (respectively):

-   ./templates
-   ./sources
-   ./API\_generated

Actually, the **extract\_sources.sh** shell script is used for
convenience. It cleans the API\_generated/ directory, creates the code,
and then builds it. The paths work for an *in source* build.

### The details

`TBD`

Code Organisation
-----------------

### API\_generated/

Not much to say, all the files here are auto-generated from the
templates.

### sources/

Here is all the source code that does not need to be inside the
templates.

<class>.dox  
This is the Doxygen description for the class, with some additional
tags.

`/** @struct  oyClass_s`  
`*  @ingroup some_group`  
`*  @extends oyStruct_s`  
`*  @brief   Brief description`  
`*  @internal`  
`*`  
`*  Multi line description`  
`*  @note New templates will not be created automaticly [notemplates]`  
`*  @note Create templates using `“`opaque`` ``pointer`”` [opaquepointer]`  
`*  @note This class holds a list of objects [list]`  
`*`  
`*  @version Oyranos: x.x.x`  
`*  @since   YYYY/MM/DD (Oyranos: x.x.x)`  
`*  @date    YYYY/MM/DD`  
`*/`

### templates/

How to import a new class
-------------------------

The following steps are used.

#### 1. Initial commit

Directory  
sources/

-   (a) cp Class.dox <class>.dox & edit
-   (b) run generator
-   (c) Edit <class>.members.h
-   (d) cp .private\_methods\_definitions.c
-   (e) run generator
-   (f) cp API\_generated/oy<class>\_s\_private\_custom\_definitions.c
    sources/<class>.private\_custom\_definitions.c
-   (g) rm
    templates/<group>/<class>\_s\_private\_custom\_definitions.template.c
-   (h) run generator

`Skip steps (c) to (h) for list classes`

git short comment  
\* Create skeleton files for oyClass\_s

#### 2. Import class members like enums,typedefs,...

oyranos/: grep 'memberof \*oy<calss>\_s' \* -B3

-   (a) Private ones in sources/<class>.private.h

git short comment  
\[sources\] Import oy<class>\_s private \[enums,typedefs,...\]

-   (b) Public ones in sources/<class>.public.h

git short comment  
\[sources\] Import oy<class>\_s public \[enums,typedefs,...\]

#### 3. Implement constructor \[oyClass\_New\]

files:  

`sources/`<class>`.private_custom_definitions.c`

git short comment  
\[review\] \[sources\] Implement the constructor for oyClass\_s

#### 4. Implement copy constructor \[oyClass\_Copy\]

sources/

`.private_custom_definitions.c`

\[review\] \[sources\] Implement the copy constructor for oyClass\_s

#### 5. Implement destructor \[oyClass\_Release\]

sources/

`.private_custom_definitions.c`

\[review\] \[sources\] Implement the destructor for oyClass\_s

#### 6. Import private methods for oyClass\_s

sources/

`.private_methods_declarations.h`  
`.private_methods_definitions.c`

\[sources\] Import private methods for oyClass\_s

#### 7. Adopt oyClass\_s private methods

sources/

`.private_methods_declarations.h`  
`.private_methods_definitions.c`

\[review\] \[sources\] Adopt oyClass\_XXX\_() to “hidden struct”
interface.

#### 8. Import public methods for oyClass\_s

sources/

`.public_methods_declarations.h`  
`.public_methods_definitions.c`

\[sources\] Import public methods for oyClass\_s

#### 9. Adopt oyClass\_s public methods

sources/

`.public_methods_declarations.h`  
`.public_methods_definitions.c`

\[review\] \[sources\] Adopt oyClass\_XXX() to “hidden struct”
interface.
