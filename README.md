# Building SoX dynamic library (libsox-3.dll) on Windows

libsox and its prerequisites libogg and libvorbis are built using autoconf in MinGW/MSYS.

## 0. Make sure you have installed MinGW/MSYS
Download and install from http://www.mingw.org.

## 1. Build libogg
1. Download libogg from https://xiph.org/downloads/. The lastest version as of this writing is 1.3.4.
2. Open a `MinGW Shell` and to the libogg folder and run
```
./configure && make
```

## 2. Build libvorbis
1. Download libvorbis from https://xiph.org/downloads/. The lastest version as of this writing is 1.3.6.
2. Open a `MinGW Shell` and go to the libvorbis folder and run (change the paths for ogg-libraries and ogg-includes to suit your locations)
```
./configure --with-ogg-libraries=Z:\vmware-share\libogg-1.3.4\src\.libs --with-ogg-includes=Z:\vmware-share\libogg-1.3.4\include\ogg --disable-oggtest && make
```

## 3. Build libsox
1. Open a `MinGW Shell` and standing in this folder run
```
./configure --without-magic --without-png --without-ladspa --without-opus --without-mad --without-libltdl --without-coreaudio --without-gsm --without-lpc10 --with-mpg123 --disable-static --enable-shared && make
```
2. The result can be found in `src/.libs/libsox-3.dll`.