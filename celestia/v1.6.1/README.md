Re-Adding a "KDE3" GUI to Celestia
==================================


The patch(es) in this directory restores the "KDE3" GUI to Celestia
(for ver. 1.6.1).  Specifically, it creates a
[TDE](https://www.trinitydesktop.org/) GUI, TDE being the desktop
environment based on a fork of KDE3.

To build it, after you've applied my patch(es), you'll need to install
the `kdelibs4-trinity-dev` package from TDE.

**Note:**  my patch quite likely includes (K)Ubuntu-specific changes.
I based my patches off of a (K)Ubuntu source package, one of an earlier
version of Celestia that still contained the KDE3 GUI.  There was
really no good way to pry out the distro-specific stuff.  It shouldn't
matter, however, if you use my patches for building Celestia for a
different Linux distro.


## Patching Instructions ##


### Direct Patch ###

`celestia-1.6.1-using_TDE.patch`


Apply in the usual way:

1. `cd` to the directory containing the `celestia-1.6.1` source code.
2. `patch -p1 celestia-1.6.1-using_TDE.patch`


### If Using Debian, Ubuntu, or `dpkg` ###

1. Do one of the following:

   1. Get the original source code tarball for `celestia-1.6.1`.
      You *might* be able to get it from a recent `dpkg` source
      package in your distribution.

   2. Rename the tarball to `celestia_1.6.1.orig.tar.gz`.

2. `cp using-deb-srcpkg/*` to whatever directory contains the
   `celestia_1.6.1.orig.tar.gz` file.

3. `cd` to the directory where you want to "install" the source code.

4. Run:
   ```
   dpkg-source -x ${debSrcPkgsDir}/celestia_1.6.1-1.dsc
   ```
   …where `${debSrcPkgsDir}` is the path containing the
   `celestia_1.6.1.orig.tar.gz` file.

   This will extract the source and apply all patches, including the
   ones containing my changes.

   * You could also directly build the binary package(s) using the
     `dpkg-source` command.  But that's left as an exercise to the
     reader.  ;)
