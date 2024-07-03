# Install Ultraleap

<!-- Do edits in README.original.md. -->

These are instructions for getting the LeapMotion SDK 2.3.1 working on Linux, Windows, and MacOS. This is for use with applications that require it to interact with the LeapMotion controller.

Ultraleap (F.K.A LeapMotion) still works really well in Linux and Windows, despite not having received an update for several years. The documentation and installation process, however, have aged a bit. This repo is here to solve that in a coherent way and will be provided to upstream.

These instructions match SDK version 2.3.1, which is currently the newest version on Linux and Mac as at 2021-11-04 (Windows is currently on 5.3.1). It is also the latest version that is known to support Java, and is still downloadable.

## Table of contents

* [Install Ultraleap](#install-ultraleap)
    * [Table of contents](#table-of-contents)
    * [Problems that this repo fixes](#problems-that-this-repo-fixes)
    * [Links](#links)
    * [Download and unpack the SDK](#download-and-unpack-the-sdk)
    * [Install](#install)
        * [Linux](#linux)
            * [Unpack the archive](#unpack-the-archive)
            * [Install on deb based distros](#install-on-deb-based-distros)
            * [Install on RPM based distros](#install-on-rpm-based-distros)
            * [Make the service start](#make-the-service-start)
            * [Testing it](#testing-it)
            * [Libraries for java applications](#libraries-for-java-applications)
        * [Windows](#windows)
            * [Install it](#install-it)
            * [Libraries for java applications](#libraries-for-java-applications)
        * [MacOS](#macos)
            * [Libraries for java applications](#libraries-for-java-applications)

<!-- table of contents created by Adrian Bonnet, see https://Relex12.github.io/Markdown-Table-of-Contents for more -->

## Problems that this repo fixes

* Reliably starting and stopping the service via systemd.
* Installation on other Linux distros.

Ultraleap are welcome to incorporate and/all of this into their instructions that they ship with the SDK.

## Links

1. [More documentation](https://developer.leapmotion.com).

## Download and unpack the SDK

NOTE that downloading the SDK requires an account, which at the time of this writing, is free.

1. Go to [Downloads](https://leap2.ultraleap.com/downloads/), and login.
1. You need "TRACKING SOFTWARE ____ 2.3.1" (Replace ____ with Linux/Windows/MacOS).
    * [Linux](https://leap2.ultraleap.com/download/software?name=tracking-software&version=2.3.1&platform=linux)
    * [Windows](https://leap2.ultraleap.com/download/software?name=tracking-software&version=2.3.1&platform=windows)
    * ~~[MacOS](https://developer.leapmotion.com/releases/mac-2-3-1)~~ - [More info](https://github.com/ksandom/installUltraleap/issues/1#issuecomment-2204932007).
1. Follow on either [Linux](#Linux), [Windows](#Windows), or [MacOS](#MacOS).

## Install

### Linux

#### Unpack the archive

1. Run `tar xzf Leap_Motion_SDK_Linux_2.3.1.tgz`
1. Run `cd LeapDeveloperKit_2.3.1+31549_linux`

#### Install on deb based distros

The packaged instructions should work as described.

`sudo dpkg --install Leap-*-x64.deb`

TODO I haven't tested this in several years. Test this.

#### Install on RPM based distros

Derived from the packaged instructions.

Tested on

* [OpenSuSE](https://www.opensuse.org/) Tumbleweed on 2021-11-04.

TODO Test others.

1. Install [alien](https://software.opensuse.org/package/alien) if you haven't already. - This converts the debs to RPMs that you can install.
    * OpenSuSE: Choose [a package](https://software.opensuse.org/package/alien).
    * Fedora: `sudo yum install alien`
1. Convert the debs by running `sudo alien -rv --scripts Leap-*-x64.deb`
1. Install the RPMs by running `sudo rpm -ivh --nodeps --force leap-*x86_64.rpm`

#### Make the service start

1. Run one of these two to get the systemd unit file and script to install it.
    * `git clone git@github.com:ksandom/installUltraleap.git`
    * `git clone https://github.com/ksandom/installUltraleap.git`
1. Run `cd installUltraleap` to get into the repo directory.
1. Run `sudo ./scripts/setupSystemd` to set it up so that it will start at boot.
1. Run `sudo systemctl start leapd` to start it now.
1. Run `sudo systemctl start leapd-resume` to make it automatically restart when your computer resumes from suspend. This is to work-around the device not always coming back into a useable state after suspend.
1. \[optional\] Run `sudo journalctl -fu leapd` to see logs.

#### Testing it

If running `LeapControlPanel` is broken for you (This is explained well in the package README.); You can run `LeapControlPanel --showsettings`

From there, there are various things of interest. I want to highlight:

* "Diagnostic Visualizer" on the "Troubleshooting" tab, which shows you a realtime 3D visualisation of what the device is reporting. (Also great fun to play with.)
* "Show Software Log" on the "Troubleshooting" tab, which tells you why something is or is not working.

You can also run `sudo journalctl -fu leapd` to see the log.

#### Libraries for java applications

The files that you will need for java applications are located in:

* LeapSDK/lib:
    * LeapJava.jar
* LeapSDK/lib/x64:
    * libLeapJava.so
    * libLeap.so

Copy these to the lib directory that the java application specifies.

### Windows

#### Install it

1. Unpack the .zip file.
1. Run `Leap_Motion_Installer_release_public_win_x86_2.3.1+31549_ah1886.exe`.

#### Libraries for java applications

The files that you will need for java applications are located in:

* LeapSDK\\lib:
    * LeapJava.jar
* LeapSDK\\lib\\x64:
    * Leap.dll
    * LeapJava.dll
    * Leap.lib

Copy these to the lib directory that the java application specifies.

### MacOS

NOTE1: I have not tested this.

NOTE2: There is a note on [the download page](https://developer.leapmotion.com/tracking-software-download) that reads:
> Not compatible with macOS Monterey

1. Unpack the .tgz file.
1. Instructions from the README.txt:
    1. Open Leap_Motion_Installer_version.dmg
    1. Run Leap Motion.pkg


#### Libraries for java applications

The files that you will need for java applications are located in:

* LeapSDK/lib:
    * LeapJava.jar
    * libLeap.dylib
    * libLeapJava.dylib

Copy these to the lib directory that the java application specifies.
