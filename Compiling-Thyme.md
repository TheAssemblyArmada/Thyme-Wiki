## Prerequisites
Thyme uses the popular CMake meta build system to generate build files for various different build engines ranging from command line systems such as make and ninja to IDE solutions for Visual Studio and XCode. To build Thyme you will first need to install CMake version 3.0 or later. On Linux you will probably be able to get a recent version from your distributions package manager. On Windows or macOS you can download it from [here](https://cmake.org/download/).

It is also recommended that you have git installed and use it to clone the repository. If CMake can find git on your system it will embed information relating to the commit you are building in the version information used in game. For Linux again the package manager should have it available. For macOS it is part of the XCode command line tools you can install by running ```xcode-select --install``` in terminal. For Windows you can download git from [here](https://git-scm.com/download/win).

## Configuring and Compiling  

### Platform Specific
[[Compiling With Visual Studio]]  
[[Compiling With Clion]]
Todo

### Generic Guide
For platforms without specific guides, the following sections should give you a good idea of what commands you need to run.

#### Downloading the source
The recommended way of obtaining the source is to clone it from GitHub. If you just want to build Thyme and run it, you can clone directly from our main repo. If you are wanting to contribute then you should fork the repository and then clone from your fork so you can create pull requests against it. Cloning using the command line is fairly straight forward and can be done with a few simple steps. This example assumes a directory called projects on Windows at the root of the C: drive:

* Open a command line terminal (git bash or cmd on Windows) and cd to the directory you will clone the respository to. ```cd C:\projects```

* Run git clone with the address of the repository from the "Clone or download" dropdown on the GitHub page. ```git clone https://github.com/TheAssemblyArmada/Thyme.git```

#### Configuring the build
CMake is used to configure the build. From the command line you will need to create a build directory and then run CMake in it. The following examples assume you cloned into C:\projects on a Windows system.

* cd to the cloned source directory. ```cd thyme```

* If you have freshly cloned the repository, run ```git submodule update --init --recursive``` to fetch the submodules the project uses.

* Make a build directory. ```mkdir build```

* cd to the new directory. ```cd build```

* Run CMake with the desired generator using the -G command and setting the type of build. ```cmake -G"Visual Studio 14 2015" -DCMAKE_BUILD_TYPE="Release" ..```

* Run CMake with just the -G and no generator name to get a list of available generators for your platform. ```cmake -G```

#### Build thyme
At this point CMake will have generated build files for you. For the example above you will have a .sln that you can load into Visual Studio or build with msbuild from the command line. Building with the 'make' command is common on other platforms.
