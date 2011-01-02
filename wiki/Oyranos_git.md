---
title: Oyranos/git
permalink: wiki/Oyranos/git/
layout: wiki
tags:
 - Oyranos
---

Git is set up on www.oyranos.org. To use git install the git-core
package.

Here is a [**download and build
script**](https://www.behrmann.name/temp/icc_examin-build.sh) to
automate the process, including a build of [ICC
Examin](/wiki/ICC_Examin "wikilink"), [CompIcc](http://compicc.sf.net) and
some requirements. The script accepts options for configure and will
pass them unchanged.

E.g. --prefix=~/.local might be a good idea to avoid the requirement
root rights for installation of a test build.

For troubleshooting and reference below are the basic single steps.

For the git version You need currently [this Elektra
version](http://www.markus-raab.org/ftp/elektra-0.7.0.tar.gz) 10:42, 29
Apr 2008 (CEST)

First check out:

`$ git clone `[`git://www.oyranos.org/git/oyranos`](git://www.oyranos.org/git/oyranos)

Oyranos relies on some certain ICC profiles by default, which are not
included in git. Take them from [OpenICC-data
package](https://sourceforge.net/projects/openicc/files/OpenICC-Profiles).

Building Oyranos:

`$ cd oyranos/`  
`$ configure`  
`$ make`  
`$ make install`

Keeping Oyranos up to date:

`$ git pull`

Examining the history:

`$ git log -p`

ICC Examin git can be obtained without the above script like follows:

`$ git clone `[`git://www.oyranos.org/git/icc_examin`](git://www.oyranos.org/git/icc_examin)

### Links

-   [git
    introduction](http://www.kernel.org/pub/software/scm/git/docs/user-manual.html#git-quick-start)
-   [Carl Worth's git tour](http://cworth.org/hgbook-git/tour/)
-   [Homepage](http://git.or.cz/) and wiki
-   [gitweb](http://www.oyranos.org/scm) of Oyranos, Xcolor and ICC
    Examin

[back -&gt; Oyranos](/wiki/Oyranos "wikilink")
