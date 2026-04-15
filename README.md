# FMOD for Godot

Welcome! This repository provides an integration of [FMOD Studio's audio middleware](https://www.fmod.com/) into the [Godot game engine](https://godotengine.org). At the moment, **FMOD version 2.03.13** and **Godot 4.6.2** are supported.

## Features

* Use the FMOD Studio API on different platforms (Windows, macOS, Linux, iOS and Android) with a [GDExtension library](https://docs.godotengine.org/en/latest/engine_details/engine_api/gdextension/what_is_gdextension.html) that seamlessly integrates with Godot and GDScript.
* Modify and build the library for any target platform with ease using SCons, a flexible and cross-platform software construction tool.
* Streamlined audio authoring workflow with FMOD Studio Live Update, which lets you sync your audio project with your game in the editor or in a build. Experiment and iterate faster without reloading or recompiling your game.
* Custom blocking I/O implementation that uses Godot's `FileAccess` API. This ensures compatibility across different platforms.
* Custom FMOD nodes, such as StudioEventEmitter3D, StudioEventEmitter2D, StudioBankLoader, StudioListener3D, StudioListener2D, StudioParameterTrigger and StudioGlobalParameterTrigger. Create an immersive audio experience for players with little code.
* Event **Timeline Marker** and **Timeline Beat** callback support to easily synchronize your game with your audio's logic. You can use these callbacks to trigger animations or gameplay events based on the timing of your audio events.
* Generate unique identifiers (GUIDs) for GDScript to maintain organization and consistency in your project. GUIDs will help you reference FMOD assets without hard-coding paths or names. 
* Search and preview Events in the Godot editor with the **FMOD Project Browser**. This handy tool lets you browse through all the Events in your project and play them back directly in the editor.
* Customize **FMOD settings** for each platform in the Godot Project Settings. You can adjust settings such as **sample rate**, **speaker mode**, **real and virtual channels**, **DSP buffer size** and more to optimize performance and quality for each platform.
* Studio API wrapper unit tests ensuring a reliable and stable integration.
* Custom performance monitors to track the performance of FMOD in the editor.

## Getting started

Extensive tutorials for the integration, including custom nodes usage and code examples can be found on the [tutorials](https://alessandrofama.com/tutorials/fmod/godot/) section of Alessandro Famà's website.

## Building

The project uses SCons to build the GDExtension library. You can build the library by navigating to the addons/FMOD/native directory and executing scons:

```bash
scons platform=windows target=template_release fmod_api="C:\\Program Files (x86)\\FMOD SoundSystem\\FMOD Studio API Windows" -j8
```

The required compilation parameters are:

* platform: `windows`, `macos`, `linux`, `android` or `ios`
* target: `template_debug` or `template_release`
* fmod_api: path to the directory that contains the api folder downloaded from fmod.com

The optional parameters are:

* target_path: specify a directory for the shared library
* dev_build: to build a library with debug symbols and no optimizations

The template_debug libraries in the GitHub releases use dev_build by default.

### Android

You need to specify the ANDROID_NDK_ROOT and arch parameters for Android:

```bash
scons platform=android target=template_debug ANDROID_NDK_ROOT=$ANDROID_NDK_LATEST_HOME arch=arm64 fmod_api=...
```

### iOS

You can pass the ios_min_version parameter to scons to specify a minimum iOS version for the library:

```bash
scons platform=ios target=template_debug dev_build=yes fmod_api=/Applications/FMOD/FMOD\ Programmers\ API\ ios ios_min_version=12.0 -j8
```

## Known issues

Known issues are being logged into the issues page of this repo. Please check this page first, then log a new issue if you haven't found it listed.

## Contributing

Any contribution is welcome. Please send pull-requests with fixes or useful additions!

## License

The integration files, code and scripts in this repository are released under the MIT license.

While this project is licensed under MIT, FMOD itself is not free and has different license schemes depending on the type and budget of your project.

You can find out more about FMOD licensing [here](https://www.fmod.com/licensing). Please make sure to obtain a license for your commercial game.
