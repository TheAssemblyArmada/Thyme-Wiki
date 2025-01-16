# CLion Bulid Guide

If you prefer to build Thyme using CLion (with the MSVC compiler), follow the instructions below. 

### Prerequisites

- **CLion** is already installed.
- **MSVC Compiler** is installed. 
    - If you haven't installed it yet, it comes with **Visual Studio 20xx**. Ensure that during Visual Studio installation, you select the **Desktop development with C++** workload to install MSVC.

### Step 1: Clone the repository using CLion's built-in VCS

1. Open CLion.
2. In the welcome window, click **Get from Version Control**.
3. Enter the repository URL: `https://github.com/TheAssemblyArmada/Thyme.git`.
4. Choose the local directory where you want to clone the repository.
5. Click **Clone** to download the source.

### Step 2: Configure CMake Profile

1. Go to **File** → **Settings** → **Build, Execution, Deployment** → **CMake**.
2. Click the **+** to add a new CMake profile.
    - Set the **Profile Name** as `x86-Debug (install)`.
    - Set the **Build Type** to `Debug`.
    - Set the **Toolchain** to `msvc_x86` (explained below).
3. To create the `msvc_x86` toolchain:
    - Click **Manage Toolchains**.
    - Click the **+** button to add a new toolchain and name it `msvc_x86`.
    - Select the folder where Visual Studio is installed (e.g., `C:\Program Files\Microsoft Visual Studio\2022\Community`).
    - Set the **Architecture** to `x86`.
    - Click **OK** to save the toolchain.
    ![Toolchain](https://github.com/user-attachments/assets/20f3b977-df12-48e5-a2d7-7ca19e7b66c6)

4. In the **CMake options**, add `-G Ninja` (Ninja is used as the default build generator).
5. In the **Build options**, add `--target install` to install the files to the game directory after building.
   
    ![CMake](https://github.com/user-attachments/assets/f6bd312b-b078-4f5c-896b-5500ea71eea0)


### Step 3: Build the project

1. Select **Run/Debug Configurations** (top-right dropdown menu).
2. Choose the `thyme.dll` target.
3. Click the **Build** button to start the compilation process. This will take a few minutes. When finished, the files will be installed in the game directory.

### Tip: Running the game directly from CLion

It is recommended to use the **[Proxy Launcher](https://gentool.net/download/tools/)** to run the game, but it is also possible to use the original executable.

To run the game directly from CLion:

1. Ensure the **Launcher** is installed in the game directory. If you haven't already, download and install it.
2. Go to **Run/Debug Configurations**.
3. Select the `thyme.dll` configuration.
4. Under **Executable**, choose the `generals.exe` file inside the **Launcher** directory. (Or choose the original executable file)
5. In **Program Arguments**, add `-win -quickstart -nologo`.
6. Enable **Run as Administrator** to ensure the game has necessary permissions.
7. Now, you can click the **Run** button or use **Debug** to run the game and view debug output in the terminal.

    ![Launcher](https://github.com/user-attachments/assets/73a54ec1-1fa4-49c6-891d-9c4fa79811e7)


---

This should guide you through building and running Thyme with CLion. If you encounter any issues, feel free to ask for assistance on our [Discord channel](https://discord.gg/YhdMbvD).
