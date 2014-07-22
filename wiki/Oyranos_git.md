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

First check out libXcm, Oyranos and then libXcm tools:

`$ git clone `[`git://github.com/oyranos-cms/xcolor`](git://github.com/oyranos-cms/xcolor)  
`$ git clone `[`git://github.com/oyranos-cms/oyranos`](git://github.com/oyranos-cms/oyranos)  
`$ git clone `[`git://github.com/oyranos-cms/xcm`](git://github.com/oyranos-cms/xcm)

Oyranos relies on some certain ICC profiles by default, which are not
included in git. Take them from [OpenICC-data
package](https://sourceforge.net/projects/openicc/files/OpenICC-Profiles).

Building Oyranos:

`$ cd oyranos/`  
`$ mkdir build && cd build/`  
`$ cmake ..`  
`$ make`  
`$ make install`

Keeping Oyranos up to date:

`$ git pull`

Examining the history:

`$ git log -p`

Some more projects:

`$ git clone `[`git://compicc.git.sourceforge.net/gitroot/compicc/compicc`](git://compicc.git.sourceforge.net/gitroot/compicc/compicc)  
`$ git clone `[`git://anongit.kde.org/kolor-manager.git`](git://anongit.kde.org/kolor-manager.git)  
`$ git clone `[`git://gitorious.org/cinepaint-ng/cinepaint-ng`](git://gitorious.org/cinepaint-ng/cinepaint-ng)

ICC Examin git can be obtained without the above script like follows:

`$ git clone `[`git://github.com/oyranos-cms/icc-examin`](git://github.com/oyranos-cms/icc-examin)

Alternative addresses for checking out over http can be found here:
[<http://Github.com/Oyranos-CMS>](http://github.com/oyranos-cms)

### Links

-   [git
    introduction](http://www.kernel.org/pub/software/scm/git/docs/user-manual.html#git-quick-start)
-   [Carl Worth's git tour](http://cworth.org/hgbook-git/tour/)
-   [Homepage](http://git.or.cz/) and wiki
-   [gitweb](http://github.com/oyranos-cms) of Oyranos,
    XColorManagement(libXcm,xcm) and ICC Examin(iccexamin)

[back -&gt; Oyranos](/wiki/Oyranos "wikilink")
