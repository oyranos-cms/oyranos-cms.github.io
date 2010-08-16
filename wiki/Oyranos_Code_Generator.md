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

#### Template system

The templates are written in the [Django template
language](http://docs.djangoproject.com/en/dev/topics/templates/). A
Django template is a plain text file with some specially formatted
**tags** and **variables**. So, a template is just a C or C++ file that
contains some extra **{% tag %}** and **{{ variable }}** embedded code
that is replaced by the code generator. This is much like *php* code is
replaced in *html* files. The built in **tags** and **variables** are
[documented
here](http://docs.djangoproject.com/en/dev/ref/templates/builtins/). The
Django template engine is written in python and can be used [in stand
alone
mode](http://docs.djangoproject.com/en/dev/ref/templates/api/#configuring-the-template-system-in-standalone-mode).
Instead, the *generator* is using the [Grantlee template
system](http://www.grantlee.org/), which uses the same template
language, but is written in C++ and depends on
[Qt](http://qt.nokia.com/).

So, how is a new source code file auto-generated?

-   First the *generator* scans the templates/ directory for template
    files. They have a special file name in the form of
    file\_name.*template*.ext, e.g. oyranos\_module.*template*.h
-   Then the various template variables are loaded (taken from the
    source code metadata) and the template is rendered in memory
-   A new file is created in API\_generated/ with the *.template.*
    removed, e.g. oyranos\_module.h

#### Template files

There are mainly two kinds of template files.

-   A [*base*](#Files "wikilink") template.
-   A *child* template that extends a *base* template. Most templates
    are *child* templates.

The *child* templates use the {% extends %} **tag**, which is how
[template
inheritance](http://docs.djangoproject.com/en/dev/topics/templates/#template-inheritance)
is implemented in the django language. There is a 1-1 relationship
between the class inheritance of the Oyranos object system and the
django template inheritance. For example, that means if *oyCMMapi10\_s*
inherits from *oyCMMapiFilter\_s*, then *CMMapi10\_s.template.c* will
extend *CMMapiFilter\_s.template.c*. And if *oyCMMapiFilter\_s* extends
*oyCMMapi\_s*, then *CMMapiFilters\_s.template.h* will extend
*CMMapi\_s.template.h*.

| Oyranos Objects   |     | Template Files             |
|-------------------|-----|----------------------------|
| oyStruct\_s       | ↔   | Struct\_s.template.h       |
|                   |     | ↑                          |
| ↑                 |     | Base\_s.h                  |
|                   |     | ↑                          |
| oyCMMapi\_s       | ↔   | CMMapi\_s.template.h       |
| ↑                 |     | ↑                          |
| oyCMMapiFilter\_s | ↔   | CMMapiFilter\_s.template.h |
| ↑                 |     | ↑                          |
| oyCMMapi10\_s     | ↔   | CMMapi10\_s.template.h     |

`The example above shows the inheritance graph for a public header file,`  
`of a common Oyranos class.`

| Oyranos Objects |     | Template Files          |
|-----------------|-----|-------------------------|
| oyStruct\_s     |     |                         |
|                 |     | Base\_s\_.c             |
| ↑               |     | ↑                       |
|                 |     | BaseList\_s\_.c         |
|                 |     | ↑                       |
| oyOptions\_s\_  | ↔   | Options\_s\_.template.c |

`The example table above shows the inheritance for a private implementation file,`  
`of a special kind of Oyranos class - a `*“`list`”*` class. Note that the `*`Base_s_.c`*  
`template does not extend a supposed `*`oyStruct_s_.template.c`*` file, because oyStruct_s`  
`only has a public interface and so no private `*`oyStruct_s_.*`*` implementation files.`

If in doubt, each generated source file has it's inheritance graph
embedded, at the top of the *@file* doxygen comment.

Code Organisation
-----------------

### File Structure

#### API\_generated/

Not much to say, all the files here are auto-generated from the
templates.

##### Classes

Each class is implemented by four files.

oyClass\_s.h  
This is the public header file that exports the class API

oyClass\_s.c  
The implementation of all the public class parts.

oyClass\_s\_.h  
Private declarations

oyClass\_s\_.c  
Private definitions

##### Modules

oyranos\_object.h  
This file includes some vital oyranos headers and also contains

definitions necessary for, but **not** part of the object system.

It is included by all the *oyClass\_s.h* headers.

oyranos\_object\_internal.h  
This file includes some private oyranos headers and definitions
necessary for,

but **not** part of the object system.

It is included by the private *oyClass\_s\_.c* implementation files.

oyranos\_generic.h  
For everything that belongs to the Generic Objects API and is not part
of a specific class.

oyranos\_generic\_internal.h  
All Generic Objects API helper code, that is for internal usage only.

It is included by all the private implementations (*oyClass\_s\_.c*
sources) that belong to

the Generic Objects group.

oyranos\_devices.h  
Exports all public declarations that are part of the Device API.

oyranos\_devices.c  
The implementation for the Device API.

oyranos\_devices\_internal.\[ch\]  
All Device API code that is for internal usage.

oyranos\_module.h  
All declarations that are part of the Module APIs, but not part of a
specific class,

and should be exported.

oyranos\_module\_internal.h  
Used for all members of the Module APIs that are not part of any class
and should not be exported.

It is included by all the private implementations (*oyClass\_s\_.c*
sources) that belong to

the Module APIs group.

oyranos\_profile.h  
All declarations that are are part of the Profile API, but not part of a
specific class,

and should be exported.

#### sources/

Here is all the source code that does not need to be inside the
templates.

##### <class>.dox

This is the Doxygen description for the class, with some additional
tags.

<code>

`/** @struct  oyClass_s`  
` *  @ingroup some_group`  
` *  @extends oyStruct_s`  
` *  @brief   Brief description`  
` *  @internal`  
` *`  
` *  Multi line description`  
` *  @note New templates will not be created automaticly [notemplates]`  
` *  @note Create templates using `“`opaque`` ``pointer`”` [opaquepointer]`  
` *  @note This class holds a list of objects [list]`  
` *`  
` *  @version Oyranos: x.x.x`  
` *  @since   YYYY/MM/DD (Oyranos: x.x.x)`  
` *  @date    YYYY/MM/DD`  
` */`

</code>

The basic idea is that the *generator* needs to know all kinds of
information **(metadata)** about the class and these are provided here.
Along with the doxygen tags, a few additional are also needed and are
put in the *@note* tag.

\[notemplates\]  
Each class has a template file for each generated source file.

At class creation, these are also created automaticly and are read-only.

When for any reason you want to override some default template block and

edit the class templates, change their permissions to read-write and

remove the \[notemplates\] tag

\[list\]  
This tag specifies that the class is a special kind of class, a *list*
of values. The

convention is that the class name is in plural *(ends with s)* and the
list item type

is the class with the same name without the *s*. E.g. oyFilterPlugs\_s
-&gt; oyFilterPlug\_s

\[opaquepointer\]  
This is an alternative way of the API and should not be used now.

##### <class>.members.h

A list of all the class members, e.g. for **CMMapi6.members.h**

<code>

` /** oyCMMapi4_s::context_type typic data; e.g. `“`oyDL`”` */`  
` char           * data_type_in;`  
` /** oyCMMapi7_s::context_type specific data; e.g. `“`lcCC`”` */`  
` char           * data_type_out;`  
` oyCMMdata_Convert_f oyCMMdata_Convert;`

</code>

##### <class>.public.h

Here goes code for the oyClass\_s.h public header file, e.g. for
**Options.public.h** <code>

`typedef oyStruct_s * (*oyStruct_Copy_f ) ( oyStruct_s *, oyPointer );`  
`typedef int       (*oyStruct_Release_f ) ( oyStruct_s ** );`  
`typedef oyPointer (*oyStruct_LockCreate_f)(oyStruct_s * obj );`  
`...`  
`extern oyStruct_LockCreate_f   oyStruct_LockCreateFunc_;`  
`extern oyLockRelease_f         oyLockReleaseFunc_;`  
`extern oyLock_f                oyLockFunc_;`  
`extern oyUnLock_f              oyUnLockFunc_;`  
`...`

</code>

##### <class>.public\_methods\_declarations.h

##### <class>.public\_methods\_definitions.c

##### <class>.private.h

##### <class>.private\_methods\_declarations.h

##### <class>.private\_methods\_definitions.c

##### <class>.private\_custom\_definitions.c

#### templates/

##### Files

###### Base\_s.h

###### Base\_s.c

###### Base\_s\_.h

###### Base\_s\_.c

###### BaseList\_s.h

###### BaseList\_s.c

###### BaseList\_s\_.h

###### BaseList\_s\_.c

###### CMakeLists.template.txt

###### oyTest.template.h / oyTest.template.cc

##### Directories

The directories are named by the group name (*@ingroup* tag) and hold
the template files of the classes that belong to that group.

### Naming conventions

#### Function prototypes

Public member functions  
All input/output variables use the public class interface. E.g:

<code>

`OYAPI oyProfile_s* OYEXPORT`  
`  oyProfile_Copy( oyProfile_s *profile, oyObject_s obj );`

</code>

Private member functions  
The input/output variables of the function class type use the private
class interface. E.g:

<code>

`oyProfile_s_*`  
`  oyProfile_Copy_( oyProfile_s_ *profile, oyObject_s object);`

</code>

  
The rest variables use their public interface. E.g:

<code>

`oyProfileTag_s * oyProfile_GetTagByPos_ ( oyProfile_s_    * profile,`  
`                                          int                 pos );`  
`int                oyProfile_TagMoveIn_ ( oyProfile_s_      * profile,`  
`                                          oyProfileTag_s   ** obj,`  
`                                          int                 pos );`

</code>

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

*`NOTE`*` Skip steps (c) to (h) for list classes.`

*`TODO`*` Implement (d) to (e) in the code generator, so that only steps (a) to (c) are needed.`

git short comment  
\* Create skeleton files for oyClass\_s

#### 2. Import class members like enums,typedefs,...

Search for them in oyranos sources  
grep 'memberof \*oy<calss>\_s' \* -B3

-   Private ones in sources/<class>.private.h
    git short comment  
    \[sources\] Import oy<class>\_s private \[enums,typedefs,...\]

-   Public ones in sources/<class>.public.h
    git short comment  
    \[sources\] Import oy<class>\_s public \[enums,typedefs,...\]

-   Add proper include files in oyClass\_s.h and oyClass\_s\_.h
    Find them by trying to compile the object files  
    cd /API\_generated/

    make oyClass\_s.o

    make oyClass\_s\_.o

    git short comment  
    \[templates\] Add include files to oyClass\_s.h

#### 3. Implement constructor \[oyClass\_New\]

files:  

`sources/`<class>`.private_custom_definitions.c`

git short comment  
\[review\] \[sources\] Implement the constructor for oyClass\_s

#### 4. Implement copy constructor \[oyClass\_Copy\]

Files:

`sources/`<class>`.private_custom_definitions.c`

git short comment  
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
