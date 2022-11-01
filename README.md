

## Building

### Windows Build Requirements
* Qt 5.15 SDK or later
* Windows 7 or later
* [Visual Studio 2019](https://visualstudio.microsoft.com/downloads/) (Community edition is fine)
* Select **MSVC 2019** option during Qt installation. MinGW is not supported.
* [7-Zip](https://www.7-zip.org/) (only if building installers for non-development PCs)
* [WiX Toolset](https://wixtoolset.org/releases/v3-14-0-5722/) v3.14.0.5722 or later (only if building installers for non-development PCs)

### macOS Build Requirements
* Qt 6.2 SDK or later
* macOS Mojave (10.14) or later
* Xcode 13
* [create-dmg](https://github.com/sindresorhus/create-dmg) (only if building DMGs for use on non-development Macs)

### Linux/Unix Build Requirements
* Qt 5.9 SDK or later
* GCC or Clang
* Install the required packages:
  * Debian/Ubuntu: `libegl1-mesa-dev libgl1-mesa-dev libopus-dev libqt5svg5-dev libsdl2-dev libsdl2-ttf-dev libssl-dev libavcodec-dev libva-dev libvdpau-dev libxkbcommon-dev qtwayland5 qt5-qmake qtbase5-dev qtdeclarative5-dev qtquickcontrols2-5-dev wayland-protocols qml-module-qtquick-controls2 qml-module-qtquick-layouts qml-module-qtquick-window2 qml-module-qtquick2`
  * RedHat/Fedora: `openssl-devel SDL2-devel SDL2_ttf-devel ffmpeg-devel qt5-qtsvg-devel qt5-qtquickcontrols2-devel libva-devel libvdpau-devel opus-devel pulseaudio-libs-devel alsa-lib-devel`
* FFmpeg 4.0+ is required to build. If your distro doesn't package FFmpeg 4.0 or later, you can build and install it from source on https://ffmpeg.org/

### Steam Link Build Requirements
* [Steam Link SDK](https://github.com/ValveSoftware/steamlink-sdk) cloned on your build system
* STEAMLINK_SDK_PATH environment variable set to the Steam Link SDK path

### Build Setup Steps
1. Install the latest Qt SDK (and optionally, the Qt Creator IDE) from https://www.qt.io/download
    * You can install Qt via Homebrew on macOS, but you will need to use `brew install qt --with-debug` to be able to create debug builds of Moonlight.
    * You may also use your Linux distro's package manager for the Qt SDK as long as the packages are Qt 5.9 or later.
    * This step is not required for building on Steam Link, because the Steam Link SDK includes Qt 5.9.
2. Run `git submodule update --init --recursive` from within `moonlight-qt/`
3. Open the project in Qt Creator or build from qmake on the command line.
    * To build a binary for use on non-development machines, use the scripts in the `scripts` folder.
        * For Windows builds, use `scripts\build-arch.bat` and `scripts\generate-bundle.bat`. Execute these scripts from the root of the repository within a Qt command prompt. Ensure WiX and 7-Zip binary directories are in your `%PATH%`.
        * For macOS builds, use `scripts/generate-dmg.sh`. Execute this script from the root of the repository and ensure Qt's `bin` folder is in your `$PATH`.
        * For Steam Link builds, run `scripts/build-steamlink-app.sh` from the root of the repository.
    * To build from the command line for development use, run `qmake moonlight-qt.pro` then `make debug` or `make release`
    * To create an embedded build for a single-purpose device, use `qmake "CONFIG+=embedded" moonlight-qt.pro` and build normally.
        * This build will lack windowed mode, Discord/Help links, and other features that don't make sense on an embedded device.

