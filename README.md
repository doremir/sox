# Building SoX dynamic library (libsox-3.dll) on Windows

libsox and its prerequisites libogg and libvorbis are built using autoconf in MinGW/MSYS.

## Prerequisites

### Install MSYS2
Download and install from https://github.com/msys2/msys2-installer.

__NOTE:__  
__On the virtual Windows 7 build machine we installed msys2-x86_64-20221028.exe which is the latest version supporting Windows 7.__

### Install MinGW-w64 etc
```
# In an MSYS2 MINGW64 Shell
pacman -S mingw-w64-x86_64-toolchain autoconf automake libtool
```

## Building dependencies
__NOTE:__  
__Instead of building the dependencies, they could probably be installed with commands like__

```
pacman -S mingw-w64-x86_64-libogg
pacman -S mingw-w64-x86_64-libvorbis
pacman -S mingw-w64-x86_64-lame
...
```

### 1. Build libogg
1. Download libogg from https://github.com/xiph/ogg. The latest version as of this writing is 1.3.5.
2. Open a `MSYS2 MINGW64 Shell` and go to the libogg folder and run
```
MAKE=mingw32-make ./configure
mingw32-make
mingw32-make install
```

### 2. Build libvorbis
1. Download libvorbis from https://github.com/xiph/vorbis. The latest version as of this writing is 1.3.7.
2. Open a `MSYS2 MINGW64 Shell` and go to the libvorbis folder and run
```
MAKE=mingw32-make ./configure
mingw32-make
mingw32-make install
```

### 2. Build libFLAC
1. Download FLAC from https://github.com/xiph/flac. The latest version as of this writing is 1.4.3.
2. Open a `MSYS2 MINGW64 Shell` and go to the FLAC folder and run
```
MAKE=mingw32-make ./configure
mingw32-make
mingw32-make install
```

### 2. Build libmpg123
1. Download libmpg123 from https://sourceforge.net/projects/mpg123/. The latest version as of this writing is 1.32.4.
2. Open a `MSYS2 MINGW64 Shell` and go to the libmpg123 folder and run
```
MAKE=mingw32-make ./configure
mingw32-make
mingw32-make install
```

### 2. Build libmp3lame
1. Download THE LATEST CODE from https://github.com/gypified/libmp3lame.
2. Open a `MSYS2 MINGW64 Shell` and go to the `libmp3lame-master` folder and run
```
MAKE=mingw32-make ./configure
mingw32-make

# NOTE:
# "mingw32-make" fails but has still linked the libmp3lame-0.dll

mingw32-make install

# NOTE:
# "mingw32-make install" fails but has still copied the libmp3lame-0.dll to /mingw64/bin/

# The lame.h file has to be copied by hand
mkdir /mingw64/include/lame/
cp include/lame.h /mingw64/include/lame/
```

### 2. Build libsndfile
1. Download libsndfile from https://github.com/libsndfile/libsndfile. The latest version as of this writing is 1.2.2.
2. Open a `MSYS2 MINGW64 Shell` and go to the libsndfile folder and run
```
MAKE=mingw32-make ./configure
mingw32-make
mingw32-make install
```

## 3. Build libsox
1. Open a `MSYS2 MINGW64 Shell` and standing in this folder run
```
autoreconf --install
MAKE=mingw32-make ./configure --without-magic --without-png --without-ladspa --without-opus --without-mad --without-libltdl --without-coreaudio --without-gsm --without-lpc10 --with-lame --with-mpg123 --disable-openmp --disable-static --enable-shared
mingw32-make
 ```
2. The result can be found in `src/.libs/libsox-3.dll`.