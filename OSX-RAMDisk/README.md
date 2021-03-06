OS X RAM Disk
================

[![Build Status](https://travis-ci.org/zafarella/OSX-RAMDisk.svg?branch=master)](https://travis-ci.org/zafarella/OSX-RAMDisk)

Need really fast Java IDE or browser? Then keep reading.

This app will create a [RAM disk](http://en.wikipedia.org/wiki/RAM_drive) in OS-X with specified size to
store the apps cache in RAM, which is known as SSD optimization - reducing disk IO or making browsing the web and
programming using IntelliJ more enjoyable.

Supported apps (you can add yours):

* [IntelliJ Idea](https://www.jetbrains.com/idea/download/)
* [Android studio](http://developer.android.com/sdk/index.html)
* [WebShtorm](https://www.jetbrains.com/webstorm/)
* [Clion](https://www.jetbrains.com/clion/)
* [AppCode](https://www.jetbrains.com/objc/)

* [PHP Storm](https://www.jetbrains.com/phpstorm/)
* [your_app_goes_here]

**You can uncomment some of the other apps, like Chrome, Safari, XCode -- Chrome is way faster if you choose to move its cache to ram disks**

* [Google Chrome](https://support.google.com/chrome/answer/95346?hl=en)
* [Google Canary](https://www.google.com/chrome/browser/canary.html)
* [Xcode](https://developer.apple.com/xcode/downloads/)
* Safari
* iTunes

The IntelliJ Idea (or JetBrains IDEs) are really fast after this. Be aware that for the large code base you will
need to have larger RAM Disk. I don't have exact numbers, sorry, it can vary because of many factors. Mine 
machine have 16GB - it works very good for small code bases.

If you observing performance degradation - revise how much memory you are using and may be adding more can help.
By default script will create RAM disk of 1/4 size of your RAM.
If you need to change the size - edit `startupRAMDiskandCacheMover.sh` header section. The RAM disk works with hibernate
option - you don't need to worry about this part.

Have something to discuss? 
[![Join the chat at https://gitter.im/zafarella/OSX-RAMDisk](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/zafarella/OSX-RAMDisk?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)

[![CII Best Practices](https://bestpractices.coreinfrastructure.org/projects/458/badge)](https://bestpractices.coreinfrastructure.org/projects/458)

Compatibility
============
Works on

* MAC OS X 10.10.2 Yosemite
* MAC OS X 10.11 EI Capitan
* MAC OS X 10.12 Sierra

> Note that you have to re-run the script in order to get the ram disk back after machine restart.
> Currently it does not place it on startup - I'm working on it.

Give it a try before installing
===============================
```bash
$ curl -o startupRAMDiskandCacheMover.sh https://raw.githubusercontent.com/ScriptedAlchemy/jetbrains-ide-performance/OSX-RAMDisk/master/Contents/MacOS/startupRAMDiskandCacheMover.sh &&
chmod +x startupRAMDiskandCacheMover.sh &&
./startupRAMDiskandCacheMover.sh
```
or
```
git clone git@github.com:ScriptedAlchemy/OSX-RAMDisk.git &&
jetbrains-ide-performance/OSX-RAMDisk/Contents/MacOS/startupRAMDiskandCacheMover.sh
```
Jetbrains IDE notes (IntelliJ)
===================
In order to speed up the compilation and responsiveness of the IDE you can
change "Project compiler output" and point it to ram disk:
```
echo /Volumes/ramdisk/${USER}/compileroutput
```
and in your project/module settings (Command+down) point to this directory.
You can also set this [setting by default](https://www.jetbrains.com/idea/help/accessing-default-settings.html) 
for your projects at the main menu, choose `File | Other Settings | Default Settings`

In addition to above you can tune jvm with following [flags](https://github.com/ScriptedAlchemy/jetbrains-ide-performance) 

Installation
============
Do not use it now - the startup script does not work yet - work in progress
```
git clone git@github.com:ScriptedAlchemy/jetbrains-ide-performance.git
cd jetbrains-ide-performance/OSX-RAMDisk
make install
```

Manual Installation
------------------
```
cp OSXRamDisk.plist ~/Library/LaunchAgents
cp startupRAMDiskandCacheMover.sh /usr/local/bin
# note - it will close Chrome, safari idea
/usr/local/bin/startupRAMDiskandCacheMover.sh
```

Uninstall
============
Run `make uninstall`
or manually do following

Close the chrome, idea or any other application you configured to use ram disk.
```
   rm /usr/local/bin/startupRAMDiskandCacheMover.sh
   launchctl unload -w ~/Library/LaunchAgents/OSXRamDisk.plist
   rm ~/Library/LaunchAgents/OSXRamDisk.plist
```

Alternatives
============
If you are Linux user use
* https://github.com/graysky2/profile-sync-daemon

-----------
Made with ♥ in NYC

