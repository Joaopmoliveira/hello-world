**Tutorial for Windows operating system with the Visual Studio IDE:**

0. In order to follow all the steps from this tutorial you must have Visual Studio installed on your machine. The version which we used was the VS 2017, but other versions should work (i.e. VS19 and VS15). If you do not have the VS program installed the steps which are presented in the following section might still have some value for you.

1. Make sure that Git is installed on your machine by typing on the command line
>\> git --version

If the output of such command is:
>git version 2.19.1.windows.1

Then you have git installed on your machine. If an error is given, then install git on your machine. 

2. To install all the necessary libraries we first need to install the vcpkg package manager (the process can be done manually but it is easier this way) which allows one to link projects with a large array of libraries already developed in C\C++. The instalation of vcpkg is trivial, you just open a command line, and write 
>\> git clone https://github.com/Microsoft/vcpkg.git
>\> cd vcpkg
>\> .\bootstrap-vcpkg.bat

3. Now we have to install the dependencies for the vkvg library which are : 
- CMake -> Used to define projects across several operating systems (OS)
- Vulkan -> The API to interact with the GPU to create images which you are already probabily familiar
- FontConfig -> The library used to find the configuration of the fonts from the OS
- Freetype -> Library used to render the fonts
- Harfbuzz -> Library used to shape the text .
- GLFW -> Library used to create a window independent from the underlying OS
To install all these libraries we can simply write (assuming you are still on vcpkg directory):
>\> vcpkg search vulkan
Which will output something like:

> angle                2019-12-31-2     A conformant OpenGL ES implementation for Windows, Mac and Linux. The goal of ...
> glad                 0.1.33-1         Multi-Language Vulkan/GL/GLES/EGL/GLX/WGL Loader-Generator based on the offici...
> glfw3                3.3.2            GLFW is a free, Open Source, multi-platform library for OpenGL, OpenGL ES and ...
> llgl                 2019-08-15       Low Level Graphics Library (LLGL) is a thin abstraction layer for the modern g...
> ms-angle             2018-04-18-2     The UWP version of a conformant OpenGL ES implementation for Windows, Mac and ...
> openxr-loader[vulkan]                 Vulkan functionality for OpenXR
> sdl2[vulkan]                          Vulkan functionality for SDL
> volk                 2019-09-26       Meta loader for Vulkan API. Note that the static library target volk::volk is ...
> vulkan               1.1.82.1-1       A graphics and compute API that provides high-efficiency, cross-platform acces...
> vulkan-hpp           2019-05-11-1     Header only C++ bindings for the Vulkan C API
> vulkan-memory-all... 2.3.0            Easy to integrate Vulkan memory allocation library from GPUOpen

> If your library is not listed, please open an issue at and/or consider making a pull request:
>    https://github.com/Microsoft/vcpkg/issues

4. So now we know that the library is currently usable from the vcpkg program so we can now write:
>\> vcpkg install vulkan

And do the same drill for all the other libraries...
>\> vcpkg install freetype
>\> vcpkg install fontconfig
>...

5. What we just did was that we download the source files from the open sourced projects and we compiled them with the MSVN compiler so we know we won't be facing any incompatibilities when compiling our tutorial. Now we can download the source code from the vkvg library by typing:

>\> cd ..

To get out of the vcpkg directory and then write:

>\> git clone https://github.com/jpbruyere/vkvg.git

6. Now we can use the IDE from CMake to generate the .sln file which can be processed by visual studio. Open the IDE and select the directory which contains the source code (it should be something like "C:\...\vkvg"). Now select the folder where you want to generate the project to. In our case we created a folder called bin ("C:\...\vkvg\bin") and selected that file. Now configure the project. This action generated a window where you can select the target build you want, in our case it is Visual Studio 15 2017 Win64 and we must specify the toolchain file for cross-compiling (because it is the vcpkg program which knowns where all the libraries we previously downloaded currently are). It should be a file located in 'C:\...\vcpkg\scripts\buildsystems\vcpkg.cmake' which contains information to be used by cmake. Now we can finish the project and if everything went well we can now select the options of the project for this specific tutorial. On the bottom of the GUI there are some options related with the VKVG libraries. You will unselect the VKVG_LCD_FONT_FILTER because we did not compile the FreeType library with this option enabled. Now press generate project and then procede to press open project. This should open the Visual Studio IDE. Now you can see the the possible built configurations.To build the project (the ALL BUILD should be the Start Up project) press F7 or press build (top of the screen) and then build solution. If everything goes well we now have a .lib and .dll folder to use in our projects.

7. The project is compiled and if you go to the 'C:\...\vkvg\bin\CMakeFiles\Debug' directory you will find all the .dlls and .libs files to integrate in your projects.

extra
