==================
installation
==================

Installation:

Unpack the compressed file.

``tar -xjvf sastbx.0.991.tar.bz2``

Change the name of the directory.

``mv sastbx-0.99-1 sastbx``

Then,

``mv sastbx/source/cctbx_src/* sastbx/source/``

``cd sastbx/build``

``python ../source/libtbx/configure.py sastbx``

``source setpaths_all.sh``

``make``

Add one line in your .bash_profile.

``source sastbx_path/build/setpaths_all.sh``
