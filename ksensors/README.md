`ksensors` with TDE Support
===========================


The patch(es) in this directory makes `ksensors` ver. 0.7.3 buildable
using TDE (the desktop environment based on a fork of KDE3).


## Instructions ##


### Direct Patch ###

`ksensors-0.7.3-using_TDE.patch`


Apply in the usual way:

* `cd` to the directory containing the `ksensors-0.7.3` source code.
* `patch -p1 ksensors-0.7.3-using_TDE.patch`


### If Using Debian, Ubuntu, or `dpkg` ###

1. Do one of the following:

   1. Get the most recent `dpkg` source package for your distribution.

      (For me, this was `ksensors-0.7.3-18ubuntu2`, but it doesn't
      matter which.)

   2. Or, get the `ksensors-0.7.3` source code tarball and rename it
      to `ksensors-0.7.3.orig.tar.gz`

2. `cp using-deb-srcpkg/*` to whatever directory contains the
   `ksensors-0.7.3.orig.tar.gz` file.

3. `cd` to the directory where you want to "install" the source code.

4. Run:

   ```
   dpkg-source -x $debSrcPkgsDir/ksensors-0.7.3-jpw1.dsc
   ```

   This will extract the source and apply all patches, including the
   ones containing my changes.
