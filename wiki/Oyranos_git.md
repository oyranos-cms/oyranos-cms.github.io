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
script**](http://www.oyranos.org/scm?p=icc_examin.git;a=blob_plain;f=icc_examin-build.sh;hb=HEAD)
to automate the process, including a build of ICC Examin, CompICC (X
Color Management spec based desktop colour server), kolor-manager (a KDE
configuration panel entry), CinePaint (a X Color Management enabled
version) and some requirements. The script accepts options for configure
and will pass them unchanged. For some options and variables see a
[**local build
script**](http://www.oyranos.org/scm?p=icc_examin.git;a=blob_plain;f=icc_examin-build-local.sh;hb=HEAD).

E.g. --prefix=~/.local might be a good idea to avoid the otherwise
required root rights for installation of a test build. For compicc one
might add similiar --plugindir=$HOME/.compiz/plugins
--icondir=$HOME/.local/share/icons --regdir=$HOME/.compiz/metadata .

Dependencies are listed in
[**README**](http://www.oyranos.org/scm?p=oyranos.git;a=blob_plain;f=README;hb=HEAD)
for some major distributions.

For troubleshooting and some reference, below are the basic single
steps. However the script will be most actual.

For the git version you need currently [this Elektra
version](http://www.markus-raab.org/ftp/elektra-0.7.0.tar.gz) 10:42, 29
Apr 2008 (CEST)

First check out libXcm and its tools:

`$ git clone `[`git://www.oyranos.org/git/xcolor`](git://www.oyranos.org/git/xcolor)  
`$ git clone `[`git://www.oyranos.org/git/xcm`](git://www.oyranos.org/git/xcm)

Then try with

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

Some more interesting projects:

`$ git clone `[`git://compicc.git.sourceforge.net/gitroot/compicc/compicc`](git://compicc.git.sourceforge.net/gitroot/compicc/compicc)  
`$ svn checkout `[`svn://anonsvn.kde.org/home/kde/trunk/playground/graphics/kolor-manager`](svn://anonsvn.kde.org/home/kde/trunk/playground/graphics/kolor-manager)  
`$ git clone `[`git://www.oyranos.org/git/cinepaint`](git://www.oyranos.org/git/cinepaint)` cinepaint`

ICC Examin git can be obtained without the above script like follows:

`$ git clone `[`git://www.oyranos.org/git/icc_examin`](git://www.oyranos.org/git/icc_examin)

Alternative addresses over http are:

`$ git clone `[`http://www.oyranos.org/git/xcolor.git`](http://www.oyranos.org/git/xcolor.git)  
`$ git clone `[`http://www.oyranos.org/git/oyranos.git`](http://www.oyranos.org/git/oyranos.git)  
`$ git clone `[`http://www.oyranos.org/git/xcm.git`](http://www.oyranos.org/git/xcm.git)  
`$ git clone `[`http://www.oyranos.org/git/icc_examin.git`](http://www.oyranos.org/git/icc_examin.git)

### Links

-   [git
    introduction](http://www.kernel.org/pub/software/scm/git/docs/user-manual.html#git-quick-start)
-   [Carl Worth's git tour](http://cworth.org/hgbook-git/tour/)
-   [Homepage](http://git.or.cz/) and wiki
-   [gitweb](http://www.oyranos.org/scm) of Oyranos, Xcolor(libXcm,xcm)
    and ICC Examin(iccexamin), cinepaint, ookala-mcf

[back -&gt; Oyranos](/wiki/Oyranos "wikilink")
