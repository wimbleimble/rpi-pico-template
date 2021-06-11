# Raspberry Pi Template for Visual Studio Code

## Prerequisite Installs
### Software:
- [ARM GCC](https://developer.arm.com/tools-and-software/open-source-software/developer-tools/gnu-toolchain/gnu-rm/downloads)
- [CMake](https://cmake.org/download/)
- [Ninja](https://ninja-build.org/)
- [Git](https://git-scm.com/download/win)
- [Visual Studio Code](https://code.visualstudio.com/download)

Most of the installers will present you with the option to "Add to path" for
either one or all users. Make sure this is selected, for conveneience later.
For Git, make sure git bash is added to the folder context menu. This can also
be done with Visual Studio Code which is helpful sometimes.

### Pico SDK
#### Downloading
Navigate to a folder in the file explorer where you want to put the SDK. Make
sure the path to the folder contains no spaces - this can cause problems
sometimes. Right click in the folder and select 'Git Bash Here'. Then paste the
following commands into the prompt, hitting enter after each:

```
git clone -b master https://github.com/raspberrypi/pico-sdk.git
cd pico-sdk
git submodule update --init
```

Git bash can then be closed.

#### Setting Environment Variables
An environment variable needs to be set so that anything that requires the
pico-sdk can find its location. To do this, press `win+r`, enter
`SystemPropertiesAdvanced` and hit enter. Then click on `Environment Variables`
and under the `User variables for ...` section select `New`. Enter the name of
the variable as `PICO_SDK_PATH` and the value as the directory of the folder
previously cloned from the git repository. For example, if the git repository
was cloned into the Documents folder of a user named `jim` on the C: drive, then
the value of the variable would be `C:\Users\jim\Documents\pico-sdk`. Press ok
on all the open dialogues then to save these settings.

## Using this Template
### Cloning
Clone this repository to the desired location by opening a Git Bash prompt as
earlier in the desired directory, and then entering:

```
git clone https://github.com/wimbleimble/rpi-pico-template
```

Then, the directory can be opened in visual studio code with the following:
```code rpi-pico-template```

Alternatively, Visual Studio Code can be opened on its own and the relevent
folder navigated to in within it.

*Note: You might want to rename the folder that `git clone` creates, as it will
otherwise always be the name of the repository ('rpi-pico-template') and if
using multiple of this template in the same folder there might be name
collisions.*

### Building
The first time you build, you need to run CMake to generate all the relevent
build files. After this is done once, Ninja will detect if CMake needs to be
rerun and do it for you, and so all builds can be done with `ctrl+shift+b` as
setup in the .vscode. To initally build CMake, open up a terminal from vscode
with `ctrl+shift+c`. Then type the following commands:
```
mkdir build
cd build
cmake -G Ninja ../src
ninja
```
This makes a directory named `build`, navigates to that directory, runs the
CMakeLists.txt file located in `src`, to generate a ninja makefile, and then
runs ninja to build this project. If you inspec the `build` directory then,
either through vscode or a file explorer, or through the command line with `dir`
then you will see the ouputted files, in particular a `main.uf2` file which can
be dragged across to the Raspberry Pi Pico to upload to the program.

*Note: you may experience an error here because the environemtn varialbe set earlier hasn't properly registered. A reboot would fix this.*

### Editing
For single file projects, the only file that needs modification (for most
things) is `Main.cpp` file located under the source directory. After editing
this to your liking, the project can then be recompiled with `ctrl+shift+b`
which just runs the command `ninja` in the build directory of the project.

For multiple file projects, the `CMakeLists.txt` file would need to be modified.