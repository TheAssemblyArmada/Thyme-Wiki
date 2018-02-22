### Additional Prerequisites

In addition to CMake and Git which are required for building on any platform, you also need a compiler suite that will convert the source code into a usable program. For windows builds, the most straight forward compiler suite is the one provided by Visual Studio, the free community edition of which can be downloaded [here](https://www.visualstudio.com/vs/community/). When installing make sure you include the C++ development tools when given the option of what components to install.

### Downloading the Source

Assuming you installed the mainline Windows Git client, open Git GUI and click "Clone Existing Respository"


[[https://user-images.githubusercontent.com/2813117/36545868-d1fbae82-17e1-11e8-9cf8-b83aa7e9be92.png|alt=Clone%20Existing]]

For the source location you want the address you get by clicking the "Clone or download" button on the main page of the github respository. The HTTPS address will probably work best. The target directory can be where ever is convenient on your system.

[[https://user-images.githubusercontent.com/2813117/36546502-8043bd76-17e3-11e8-8ebd-748c2c5edb81.png|alt=Clone%20Settings]]

Now just click the "Clone" button and wait for the download to complete.

### Configuring with CMake

Open CMake (cmake-gui) and either browse to the directory that you cloned the repository to or just type it for the "Where is the source code" box. For the "Where to build the binarys" box we recommend that you use a subdirectory under the folder that you cloned to called "build" as in the screen shot below.

[[https://user-images.githubusercontent.com/2813117/36568134-c4a695e6-1820-11e8-885c-2a1f51e06769.png|alt=CMake%20Paths]]

Click the "Configure" button and select the appropriate Visual Studio generator, either 2015 or 2017. To build a working .dll file, do not try to use the Win64 generators.

[[https://user-images.githubusercontent.com/2813117/36568247-2d2e0284-1821-11e8-9343-c2c79f45db90.png|alt=CMake%20Generator]]

CMake will do some testing to check you have working compilers installed and try and detect any required development libraries such as the Direct3D SDK. Once complete, the main window of CMake will fill with the various parameters that will be used as part of the build. Provided there were no errors, this configuration shouldn't need any tweaking, so go ahead and click "Generate". This should generate a solution that you can load into Visual Studio in the build directory we specified initially in the CMake window.

### Compiling the Code

Open Visual Studio and use the normal file open menu to find the .sln solution file that CMake generated in the build directory and open it. Select the "Build" menu item and "Build Solution" and the project should compile. When its finished under your build directory should be a directory named after the type of build (Debug, Release, RelWithDebInfo) containing thyme.dll and launchthyme.exe.
