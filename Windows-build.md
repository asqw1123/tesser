These instructions show how to build Tesseract for Windows using a build standard based on the _GNU autotools_. Other methods use _cmake_ with either the _GNU compiler_ or _Microsoft Visual Studio_. Those other methods are not covered here.

# Cross building from Debian GNU Linux

Cross building means that we compile on Linux, but the resulting programs will run on Windows.
This is our preferred way to build Tesseract for Windows because it is much faster than a native build on Windows.
The instructions here are for Debian GNU Linux, but also work for other Debian based Linux distributions like for example Ubuntu. Other Linux distributions need more or less modifications of these instructions.

## Preconditions

Several packages are needed to allow builds with the _GNU autotools_. Let's make sure that we have installed them:

    apt install TODO

In addition, we need the cross tools for building Windows programs:

    apt install TODO

Finally, several pre-compiled libraries for Windows are needed.
Those libraries are not part of Debian GNU Linux, so we use Cygwin packages which were converted to Debian packages.
TODO.

    dpkg -i TODO

## Get and build Leptonica

    cd $HOME
    mkdir -p src/github/DanBloomberg
    cd src/github/DanBloomberg
    git clone git@github.com:DanBloomberg/leptonica.git
    cd leptonica
    ./autobuild
    mkdir -p bin/ndebug/i686-w64-mingw32
    cd bin/ndebug/i686-w64-mingw32
    ../../../configure  --host=i686-w64-mingw32 --prefix=/usr/i686-w64-mingw32 CFLAGS='-Wall -Wextra -pedantic -g -O2'
    make
    sudo make install

## Get and build Tesseract

TODO.
