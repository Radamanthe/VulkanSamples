# Vulkan Samples
  - This repository is a collection of Vulkan C++ sample applications.
  - Run the following script to obtain a short description of all or a 
    specific sample:
    `$ src/get-short-descripts.sh`
  - Run the following script to obtain a more detailed description of all
    samples with a long description set:
    `$ src/get-descripts.sh`

## Structure
  - The Vulkan Samples repo is a set of source and data files in a specific
    directory hierarchy:
      - API-Samples - Samples that demonstrate the use of various aspects of the
        Vulkan API
      - Sample-Programs - Samples that are more functional and go deeper than simple API use.
      - Layer-Samples - Samples that are implemented as layers.
      - Android-Only - Samples that are only meant to be run on Android

## Sample progression
  - In general, the samples are not interrelated, but there is a progression
      among some of the samples that lead to drawing a cube.  Start with the
      instance sample, then enumerate-adv, device, initcommandbuffer, initswapchain, initdepthbuffer,
      inituniformbuffer, descriptor_pipeline_layouts, initrenderpass, initshaders,
      initframebuffers, vertexbuffer, allocdescriptorsets, initpipeline, and they
      culminate in the drawcube sample.  Each sample uses utility routines from
      the code from previous samples to get to the point to show something new.
      The drawtexturedcube sample takes all of the drawcube code and adds texturing.

## Clone the Repository

The VulkanSamples repository also includes the Vulkan loader, validation layers, header files, and associated tests.
These files are mirrored from this GitHub repository:
https://github.com/KhronosGroup/Vulkan-LoaderAndValidationLayers
These components are required to enable this repository to be built standalone; that is without having to clone the Vulkan-LoaderAndValidationLayers repository.

To create your local git repository of VulkanSamples:
```
cd YOUR_DEV_DIRECTORY
git clone git@github.com:LunarG/VulkanSamples.git
cd VulkanSamples
# This will fetch and build glslang and spriv-tools
./update_external_sources.sh         # linux
./update_external_sources.bat --all  # windows
```
## Linux Build

Example debug build:
```
cd YOUR_DEV_DIRECTORY/VulkanSamples  # cd to the root of the VulkanSamples git repository
cmake -H. -Bdbuild -DCMAKE_BUILD_TYPE=Debug
cd dbuild
make
```
## Android:

```
$ cmake -DANDROID=ON -DANDROID_ABI=[armeabi-v7a|arm64-v8a| x86|x86_64|all(default)]
```
And import VulkanSamples/API-Samples/android/build.gradle in Android Studio.

## Windows System Requirements

Windows 7+ with additional required software packages:

- Microsoft Visual Studio 2013 Professional.  Note: it is possible that lesser/older versions may work, but that has not bee
n tested.
- CMake (from http://www.cmake.org/download/).  Notes:
  - Tell the installer to "Add CMake to the system PATH" environment variable.
- Python 3 (from https://www.python.org/downloads).  Notes:
  - Select to install the optional sub-package to add Python to the system PATH environment variable.
  - Need python3.3 or later to get the Windows py.exe launcher that is used to get python3 rather than python2 if both are i
nstalled on Windows
- Git (from http://git-scm.com/download/win).
  - Tell the installer to allow it to be used for "Developer Prompt" as well as "Git Bash".
  - Tell the installer to treat line endings "as is" (i.e. both DOS and Unix-style line endings).
- glslang is required to compile glsl to spirv and should be obtained by running update_external_sources

## Windows Build

To build all Windows targets (e.g. in a "Developer Command Prompt for VS2013" window):
```
cd VulkanSamples  # cd to the root of the VulkanSamples git repository
mkdir build
cd build
cmake -G "Visual Studio 12 Win64" ..
```

At this point, you can use Windows Explorer to launch Visual Studio by double-clicking on the "VULKAN.sln" file in the \buil
d folder.  
Once Visual Studio comes up, you can select "Debug" or "Release" from a drop-down list.  
You can start a build with either the menu (Build->Build Solution), or a keyboard shortcut (Ctrl+Shift+B).
As part of the build process, Python scripts will create additional Visual Studio files and projects,
along with additional source files.  
All of these auto-generated files are under the "build" folder.

Vulkan programs must be able to find and use the Vulkan-1.dll library.
Make sure it is either installed in the C:\Windows\System32 folder,
or the PATH environment variable includes the folder that it is located in.

### Windows 64-bit Installation Notes
If you plan on creating a Windows Install file (done in the windowsRuntimeInstaller sub-directory) you will need to build fo
r both 32-bit and 64-bit Windows since both versions of EXEs and DLLs exist simultaneously on Windows 64.

To do this, simply create and build the release versions of each target:
```
cd VulkanSamples  # cd to the root of the Vulkan git repository
mkdir build
cd build
cmake -G "Visual Studio 12 Win64" ..
msbuild ALL_BUILD.vcxproj /p:Platform=x64 /p:Configuration=Release
mkdir build32
cd build32
cmake -G "Visual Studio 12" ..
msbuild ALL_BUILD.vcxproj /p:Platform=x86 /p:Configuration=Release
```

## Contributing
  Refer to the README.contrib file for specific info regarding contributing to
  the Vulkan samples creation effort.
