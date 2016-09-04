# Leksah, an Integrated Development Environment for Haskell

[![Build Status](https://secure.travis-ci.org/leksah/leksah.png)](http://travis-ci.org/leksah/leksah)

[Leksah](http://leksah.org/) aims to integrate various Haskell development
tools to provide a practical and pleasant development environment.
The user interface is a mix of GTK+ and WebKit based components.

Documentation can be found on [leksah.org](http://leksah.org/).

## Getting Leksah
Leksah requires you have **ghc >= 7.10.3** and **cabal-install >= 1.24** installed

* **Windows** and **OS X**: [official binaries](https://github.com/leksah/leksah/wiki/download).
* **Linux**: [Build from source](https://github.com/leksah/leksah#building-from-source)
   
## Building from source

Requirements: ghc >= **7.10.3**, cabal-install >= **1.24**

We have just completed a port of Leksah from Gtk2Hs to haskell-gi.  Not all
of the code is in Hackage yet so to build it you can either use [Xobl](xobl/Readme.md)
or follow the instructions below.

**Step 1**. Install the following C libraries

##### Fedora
`sudo dnf install gobject-introspection-devel webkitgtk3-devel gtksourceview3-devel`

##### Ubuntu
`sudo apt-get install libgirepository1.0-dev libwebkitgtk-3.0-dev libgtksourceview-3.0-dev`

##### Arch Linux
`sudo pacman -S gobject-introspection gobject-introspection-runtime gtksourceview3 webkitgtk`

##### OS X MacPorts
`sudo port install gobject-introspection webkit-gtk3-devel gtksourceview3`

You will also need to build a MacPorts compatible of GHC.  First install GHC some other way then unpack the source for the GHC version you want to use and run:

    sudo port install libxslt gmp ncurses libiconv llvm-3.5 libffi
    ./configure --prefix=$HOME/ghc-8.0.1 --with-iconv-includes=/opt/local/include --with-iconv-libraries=/opt/local/lib --with-gmp-includes=/opt/local/include --with-gmp-libraries=/opt/local/lib --with-system-libffi --with-ffi-includes=/opt/local/lib/libffi-3.2.1/include --with-ffi-libraries=/opt/local/lib --with-nm=/Applications/Xcode.app/Contents/Developer/Toolchains/XcodeDefault.xctoolchain/usr/bin/nm-classic
    make
    make install

Then make sure the $HOME/ghc-8.0.1 is in your $PATH.

##### OS X Homebrew
Homebrew Does not have WebKitGTK 2.4.x (newer versions of WebKitGTK only have WebKit 2 interface)

##### Windows MSYS2
Install [MSYS2](https://msys2.github.io/) and [Chocolatey](https://chocolatey.org/).  Then in a shell with administrator privileges:

    choco install ghc
    pacman -S mingw64/mingw-w64-x86_64-pkg-config mingw64/mingw-w64-x86_64-gobject-introspection mingw64/mingw-w64-x86_64-gtksourceview3 mingw64/mingw-w64-x86_64-webkitgtk3


**Step 2**: Install tools

    cabal update
    cabal install alex happy
    cabal install haskell-gi

(make sure `~/.cabal/bin` is in PATH)

**Step 3**: Clone the repo

    git clone --recursive https://github.com/leksah/leksah.git
    cd leksah

**Step 4**: Build and Run Leksah

    ./leksah.sh

On OS X using MacPorts you may need to set `XDG_DATA_DIRS` like this:

    XDG_DATA_DIRS=/opt/local/share cabal new-build exe:leksah-server exe:leksah

#### Using `stack build` instead of `cabal new-build`

** NOTE : This is currently not working.  If you can make it work let us know how you did it. **
