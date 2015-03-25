Porting the Celestia "KDE3" GUI to TDE
======================================


The patch(es) in this directory ports Celestia's old "KDE3" GUI
(for ver. 1.6.1) to [TDE-r14](https://www.trinitydesktop.org/).

To build it, after you've applied my patch(es), you'll need to install
the following TDE packages:
* libtqtinterface-dev
* libtqt3-mt-dev
* tdelibs14-trinity-dev


**Note:**  Everything in this directory is based on the Ubuntu source
packages from (K)Ubuntu v14.04LTS.
I've had to keep the same package-name as the original Ubuntu package, adding
a peculiar custom prefix so that `apt-get` will treat my custom pacakge as
an upgrade and not a downgrade.


## Patching Instructions ##

1. Change to the directory where you want to build your patched package,
   then run: `apt-get source celestia`.

2. `cp for-deb-srcpkg/*` to whatever directory contains the
   `celestia_1.6.1.orig.tar.gz` file.

3. Run:
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
