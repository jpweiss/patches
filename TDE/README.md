Patches to TDE Components
=========================


Right now, there's only one patch here:


## `ksysguardd` for Modern Linux Kernels ##

The Linux Kernel deprecated `/proc/acpi` some time ago.  The
hardware information that used to live here has long since moved into
the `/sys` filesystem.  As `/proc/acpi` continues to vanish, the
[TDE](https://www.trinitydesktop.org/) version of `ksysguardd` grows
increasingly out-of-date.  As of linux v3.13, power-source information
has "vanished" — a definite problem for laptops.

To remedy this problem, I've looked in the `ksysguardd` source for
what it tries to read from `/proc/acpi`, then hunted down the
corresponding file in `/sys`.  I then patched the source to look for
the information in *both* filesystems.

Now, because `ksysguardd` is just a background daemon, you can compile
it on its own:

1. Download the `kdebase-trinity-3.5.13` source code and untar.  (Or,
install its source-package.)

2. `cd` to the source-code directory for `kdebase-trinity-3.5.13`,
then apply the patch:
```
patch -p1 ksysguardd-TDE-3.5.13.patch
```

3. Prepare the source code for building:

   * _WARNING_:  You will, unfortunately, need to install some (or
     all?) of the libraries and development packages that
     `kdebase-trinity-3.5.13` needs … even though you need **none** of
     them to compile `ksysguardd`.

   * I might *eventually* provide workaround-`Makefile`s to make it
     possible to compile `ksysguardd` without having to configure all
     of `kdebase-trinity`.

   * You can, if you want, use CMake to set up the build-environment.
     I've provided a convenient script for running CMake.  Just source
     it from inside of the `kdebase-trinity-3.5.13` source-code
     directory:
     ```
     . ${PathToTheScript}/cmake-trinity-setup
     ```

   * Or, you can try this:
     ```
     cp -Rp /usr/share/aclocal/libtool.m4 admin/libtool.m4.in
     cp -Rp /usr/share/libtool/config/ltmain.sh admin/ltmain.sh
     make -f admin/Makefile.common
     ./configure
     ```
     However, TDE is deprecating this configuration method in favor of
     CMake.

4. Build *just* the `ksysguardd` daemon:
   ```
   cd ksysguard/ksysguardd
   make
   ```

5. Copy the new binary to someplace central, appending `.sysfs` to its
   name.  (This way, the name tells you it's the customized version.)
   For example, you could do this:
   ```
   sudo cp ksysguardd /usr/local/bin/ksysguardd.sysfs
   ```

6. Now, "swap out" the default TDE `ksysguardd` binary for the one you
   just built:
   ```
   cd ${TDEBASE}/bin
   sudo mv ksysguardd ksysguardd.trinity
   sudo ln -s /usr/local/bin/ksysguardd.sysfs ksysguardd
   ```
   …where `${TDEBASE}` is the location where TDE is installed, usually
   `/usr/local/trinity` or `/opt/trinity`.

   (If you want, you can put `ksysguardd.sysfs` directly into
   `/opt/trinity/bin` and symlink accordingly.)

Well, that, at least, is how *I* do it.
