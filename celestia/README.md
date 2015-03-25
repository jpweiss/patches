Re-Adding a "KDE3" GUI to Celestia
==================================


These patches restore the "KDE3" GUI to Celestia v1.6.1.  Specifically,
it creates a [TDE](https://www.trinitydesktop.org/) GUI, TDE being the
desktop environment based on a fork of KDE3.

The `v1.6.1` subdirectory contains a patch against the base-source coder
for Celestia v1.6.1.  However, it's designed to build against older versions
of TDE.

The `v1.6.1-ubuntu` subdirectory contains the patch against the source-package
from Ubuntu 14.04 LTS.  The patch contains a more complete port of Celestia
to TDE, specifically TDE-r14.


(I intend to reorganize everything here at a later date, when I have the
time to do so.)
