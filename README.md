# Building XDF Browser

This file includes quick start recipes. To see general principles, look at the LSL documentation:
https://labstreaminglayer.readthedocs.io/dev/build_env.html

## Windows - CMake - Visual Studio 2017

Starting with Visual Studio 2017, Microsoft began to support much closer integration with CMake. Generally, this uses the Visual Studio GUI as a wrapper around the CMake build files, so you should not expect to see most of the Visual Studio Project configuration options that you are familiar with, and CMake projects cannot be directly blended with non-CMake Visual Studio projects. There are also some weird gotchas, described below.

You will need to download and install:<BR/>
 * [The full LabStreamingLayer meta project](https://github.com/labstreaminglayer/labstreaminglayer) -> Clone (include --recursive flag) or download
 * [Visual Studio Community 2017](https://imagine.microsoft.com/en-us/Catalog/Product/530)
 * [CMake 3.12.1](https://cmake.org/files/v3.12/)
 * [Qt 5.11.1](https://download.qt.io/archive/qt/5.11/)
 * [Boost 1.65.1](https://sourceforge.net/projects/boost/files/boost-binaries/1.65.1/boost_1_65_1-msvc-14.1-32.exe/download)

From Visual Studio:<BR/>
 * File -> Open -> CMake -> labstreaminglayer/CMakeLists.txt
 * Wait while CMake configures automatically and until CMake menu turns black
 * Select x86-Release
 * CMake menu -> Change CMake Settings -> LabStreamingLayer

Add the "variable" section to the x86-Release group, so that it looks approximately like this:
```
{
  "name": "x86-Release",
  "generator": "Ninja",
  "configurationType": "RelWithDebInfo",
  "inheritEnvironments": [ "msvc_x86" ],
  "buildRoot": "${env.USERPROFILE}\\CMakeBuilds\\${workspaceHash}\\build\\${name}",
  "installRoot": "${env.USERPROFILE}\\CMakeBuilds\\${workspaceHash}\\install\\${name}",
  "cmakeCommandArgs": "",
  "buildCommandArgs": "-v",
  "ctestCommandArgs": "",
  "variables": [
    {
      "name": "Qt5_DIR",
      "value": "C:\\Qt\\5.11.1\\msvc2015\\lib\\cmake\\Qt5 "
    },
    {
      "name": "BOOST_ROOT",
      "value": "C:\\local\\boost_1_65_1"
    },
    {
      "name": "LSLAPPS_XDFBrowser",
      "value": "ON"
    }
  ]
}
```

 * Also consider changing the build and install roots, as the default path is obscure. When you save this file, CMake should reconfigure, and show the output in the output window (including any CMake configuration errors).
 * Note that it is not a typo that Qt refers to msvc2015 rather than msvc2017.

 * Select Startup Item (green arrow dropdown) -> XDFBrowser.exe (Install)

 * Click the green arrow. The application should launch.

Note that if you change Qt versions, or other significant changes, it will be necessary to do a full rebuild before CMake correctly notices the change. CMake -> Clean All is not sufficient to force this.

Just deleting the build folder causes an unfortunate error (build folder not found) on rebuild. To do a full rebuild, it is necessary to change the build and install folder paths in CMake -> Change CMake Settings -> LabStreamingLayer, build, then delete the old folder, change the path back, and build again.

## Windows - CMake - Legacy

This procedure also works in Visual Studio 2017, if desired. Generally, I'd recommend sticking with the newer procedure and Visual Studio 2017.

This procedure generates a Visual Studio type project from the CMake files, which can then be opened in Visual Studio.

You will need to download and install:<BR/>
 * The full [LabStreamingLayer meta project](https://github.com/labstreaminglayer/labstreaminglayer) -> Clone (include --recursive flag) or download
 * Desired Visual Studio Version (the example uses 2015).
 * [CMake 3.12.1](https://cmake.org/files/v3.12/)
 * [Qt 5.11.1](https://download.qt.io/archive/qt/5.11/)
 * [Boost 1.65.1](https://sourceforge.net/projects/boost/files/boost-binaries/1.65.1/boost_1_65_1-msvc-14.1-32.exe/download)


From the command line, from the labstreaminglayer folder:<BR/>
 * labstreaminglayer\build>cmake .. -G "Visual Studio 14 2015" -DQt5_DIR="C:/Qt/5.11.1/msvc2015/lib/cmake/Qt5" -DBOOST_ROOT=C:\boost\boost_1_65_1 -DLSLAPPS_XDFBrowser=ON
 * labstreaminglayer\build>cmake --build . --config Release --target install

To see a list of possible generators, run the command with garbage in the -G option.

The executable is in labstreaminglayer\build\install\XDFBrowser.

You can open the Visual Studio Project with labstreaminglayer\build\LabStreamingLayer.sln.

The command line install feature does not put build products in the sample place as when you build inside of Visual Studio. To get running to work inside of Visual Studio, it is necessary to copy the support files from labstreaminglayer\build\install\XDFBrowser to labstreaminglayer\build\Apps\XDFBrowser\Release. You must also right click XDFBrowser -> Set as Startup Project and select Release and Win32.<BR/>

If any significant changes are made to the project (such as changing Qt or Visual Stuido version) it is recommended that you delete or rename the build folder and start over. Various partial cleaning processes do not work well.<BR/>

## Linux

To be written

## OS X

To be written
