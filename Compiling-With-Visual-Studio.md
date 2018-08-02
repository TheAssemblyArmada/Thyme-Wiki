# Requirements
In order to build Thyme, you need to download and install the following programs:

- Windows 7 / 8 / 10
- [Git client](https://git-scm.com/downloads)
- [CMake](https://cmake.org/download/)
- Visual Studio 2017 or above: Enterprise, Professional or [Community (Free)](https://www.visualstudio.com/vs/community/) version
- [DirectX8 SDK (august 2007)](https://www.microsoft.com/en-gb/download/details.aspx?id=13287)

## Visual Studio additional notes

When installing make sure you include the C++ development tools when given the option of what components to install. Also, make sure to update Visual Studio to the latest version to prevent potential problems.

# Building Thyme

## Downloading the source using git

*Note: this could also be done by using [GitHub Desktop](https://desktop.github.com/), but in this guide we will asume you used the Git client.*

1. Assuming you installed the mainline Windows Git client, open Git GUI.
2. Click on "Clone Existing Respository"

[[https://user-images.githubusercontent.com/2813117/36545868-d1fbae82-17e1-11e8-9cf8-b83aa7e9be92.png|alt=Clone%20Existing]]

3. Enter the source location and the target directory. For the source location you want 'https://github.com/TheAssemblyArmada/Thyme.git'.
4. Enter in the target directory. This can be where ever is convenient on your system.

[[https://user-images.githubusercontent.com/2813117/43591552-85f9e4f0-966b-11e8-858b-6ee45639ec90.png|alt=Clone%20Settings]]

5. Now just click the "Clone" button and wait for the download to complete.

## Configuring with CMake

6. Open CMake (cmake-gui).
7. Either browse to the directory that you cloned the repository to (target directory) or just type it for the "Where is the source code" box.
8. For the "Where to build the binarys" box we recommend that you use a subdirectory under the folder that you cloned to called "build" as in the screen shot below.

[[https://user-images.githubusercontent.com/2813117/36568134-c4a695e6-1820-11e8-885c-2a1f51e06769.png|alt=CMake%20Paths]]

9. Click the "Configure" button.
10. Select the appropriate Visual Studio generator, either 2015 or 2017. This depends on which version of Visual Studio you previously installed. *Do not try to use the Win64 generators as this will produce a malfunctioning build.*
11. Click on "Finish." *CMake will now do some testing to check you have working compilers installed and try and detect any required development libraries, such as the previously installed DirectX SDK.*

[[https://user-images.githubusercontent.com/2813117/36568247-2d2e0284-1821-11e8-9343-c2c79f45db90.png|alt=CMake%20Generator]]

12. *Once complete, the main window of CMake will fill with the various parameters that will be used as part of the build. Provided there were no errors, this configuration shouldn't need any tweaking* If you see any errors you're not able to solve, contact us through our [Discord channel](https://discord.gg/YhdMbvD).
13. Now, go ahead and click "Generate". *This should generate a solution that you can load into Visual Studio in the build directory we specified initially in the CMake window.*

## Compiling the Code

14. Open Visual Studio 2017.
15. Use the normal file open menu to find the .sln solution file that CMake generated in the build directory and open it.
16. Select the "Build" menu item and lick on "Build Solution". Now the project should compile. *This can take a few minutes. When its finished, under your build directory should be a directory named after the type of build (Debug, Release, RelWithDebInfo). This directory contains your compiled 'thyme.dll' and 'launchthyme.exe'.*

## Troubleshooting

### "S1023" error at the end of the installation of the DirectX SDK.

At the end of the installation of the DirectX SDK a "S1023" could pop up. This error can be ignored and everything will be fine. But if you want to fix it, [these instructions](https://support.microsoft.com/en-us/help/2728613/s1023-error-when-you-install-the-directx-sdk-june-2010) can be followed.
