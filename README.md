# Install UltraMotion Gemini

Ultramotion Gemini (F.K.A LeapMotion) still works really well in Linux, despite not having received an update for several years. The documentation and installation process, however, have aged a bit. This repo is here to solve that and will be provided to upstream.

These instructions match SDK version Version 2.3.1, which is current on Linux and Mac as at 2021-11-04. Windows is currently on 5.2.0.

## Problems that this repo fixes

* Reliably starting and stopping the service via systemd.
* Installation on other distros.

## Overview

1. [Download and unpack the SDK](#download-and-unpack-the-sdk).
1. Install.
  * [Install on deb based distros](#install-on-deb-based-distros). (Eg Ubuntu and Debian)
  * [Install on RPM based distros](#install-on-RPM-based-distros). (Eg OpenSuSE and Fedora)
1. [Make the service start](#make-the-service-start).
1. [Testing it](#testing it).
1. [More documentation](https://developer.leapmotion.com).

## Download and unpack the SDK

NOTE that downloading the SDK requires an account, which at the time of this writing, is free.

1. Go to [https://developer.leapmotion.com/](https://developer.leapmotion.com/).
1. Click "Download Ultraleap Gemini".
1. Choose your operating system. (These instructions assume Linux.)
1. Run `tar xzf Leap_Motion_SDK_Linux_2.3.1.tgz`
1. Run `cd LeapDeveloperKit_2.3.1+31549_linux`

## Install

### Install on deb based distros

The packaged instructions should work as described.

`. sudo dpkg --install Leap-*-x64.deb`

TODO I haven't tested this in several years. Test this.

### Install on RPM based distros

Tested on

* [OpenSuSE](https://www.opensuse.org/) Tumbleweed .

1. Install [alien](https://software.opensuse.org/package/alien) if you haven't already. - This converts the debs to RPMs that you can install.
1. Convert the debs by running `sudo alien -rv --scripts Leap-*-x64.deb`
1. Install the RPMs by running `sudo alien -rv --scripts Leap-*-x64.deb`

## Make the service start

## Testing it
