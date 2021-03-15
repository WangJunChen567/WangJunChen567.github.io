---
layout: post
title: Build Qt and VTK Environment Using Visual Studio and CMake
date: 2021-03-11 20:25:00 +0800
description: Instructions on how to use Qt and VTK in Visual Studio 2019
img: vtk-qt-vs-cmake.png
tags: [VTK, Qt, Visual Studio, CMake, Local environment]
---

VTK is a powerful scientific visualization C++ library that officially provides a Qt interface. Both VTK and the latest Qt recommend using CMake to build projects. Meanwhile, the Visual Studio team has developed a fairly easy to use environment for CMake projects. All the above conditions make it easy to develop GUIs with rich widgets and high performance graphics in the best C++ IDE available .

## 1. Install Visual Studio 2019 and CMake component

Make sure that **C++ CMake tools for Windows** is checked in **Individual components**.

## 2. Install Qt and add system environment variables

After the installation of Qt, add a new system variable named **QT_DIR** and record the Qt library path (e.g., **D:\Qt\5.15.2\msvc2019_64**). After that, append **%QT_DIR%/bin** and **%QT_DIR%/lib** to the **Path** system variable.

## 3. Install VTK and add system environment variables

Download and extract the source files of the VTK library, then insert the following in the CMakeLists.txt file in its root directory
```cmake
set(VTK_MODULE_ENABLE_VTK_RenderingContextOpenGL2 YES)
```

Next, open the root directory in Visual Studio, add **Debug** and **Release** in **Manage Configurations**. In each configuration
- Wait until the table of cmake variables appear, then change the value of **CMAKE_INSTALL_PREFIX** to your desired VTK library path (e.g., **E:\VTK**), and change the value of **VTK_GROUP_ENBALE_Qt** to **WANT**, then save;
- Wait until the table of cmake variables is refreshed, then change the value of **QT5_DIR** to the path containing the main CMake file of Qt (e.g., **D:/Qt/5.15.2./msvc2019_64/lib/cmake/Qt5**) and save;
- Wait until the CMake generation finished, then toggle **Swith Views** in **Solution Explorer** so that you can double-click to switch to **CMake Target View**, where you can right-click on the project and select **Install**.

After the installation of VTK library in both **Debug** and **Release** configurations, add a new system variable named **VTK_DIR** and record the path to the VTK library (e.g., **E:\VTK**). After that, append **%VTK_DIR%/bin** to the **Path** system variable.

## 4. Use Qt and VTK in a CMake project

Find the Qt library
```cmake
#======================= INCLUSION OF Qt =======================#
set(CMAKE_INCLUDE_CURRENT_DIR ON)
set(CMAKE_AUTOMOC ON)
set(CMAKE_AUTOUIC ON)
set(CMAKE_PREFIX_PATH $ENV{QT_DIR})
find_package(OpenGL)
find_package(Qt5Core REQUIRED)
find_package(Qt5Gui REQUIRED)
find_package(Qt5OpenGL REQUIRED)
find_package(Qt5Xml REQUIRED)
find_package(Qt5Widgets REQUIRED)
``` 

Find the VTK library
```cmake
#======================= INCLUSION OF VTK ======================#
set(VTK_DIR $ENV{VTK_DIR})
find_package(VTK REQUIRED)
```

Link the QT and VTK library
```cmake
#===================== LINKING LIBRARIES =======================#
target_link_libraries(your_project_name Qt5::OpenGL)
target_link_libraries(your_project_name Qt5::Xml)
target_link_libraries(your_project_name Qt5::Widgets)
target_link_libraries(your_project_name ${OPENGL_LIBRARIES})
target_link_libraries(your_project_name ${VTK_LIBRARIES})

vtk_module_autoinit(
    TARGETS your_project_name
    MODULES ${VTK_LIBRARIES}
    )
```
