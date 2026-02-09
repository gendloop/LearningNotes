# Chore

## 添加版本号

1. [https://blog.csdn.net/qq295109601/article/details/118063009](https://blog.csdn.net/qq295109601/article/details/118063009)
2.

```cmake
在 Windows 平台上，可以使用资源文件 (.rc) 为可执行文件添加版本信息。CMake 支持使用 `configure_file()` 命令来生成 .rc 文件，并将其添加到可执行文件中。

下面是一个示例 CMakeLists.txt 文件，其中添加了版本信息：

```

cmake_minimum_required(VERSION 3.5)

project(MyProject VERSION 1.0.0)

# Configure version.rc file

configure_file(
  "${CMAKE_CURRENT_SOURCE_DIR}/version.rc.in"
  "${CMAKE_CURRENT_BINARY_DIR}/version.rc"
  @ONLY
)

# Add version.rc file to executable

add_executable(MyExecutable main.cpp "${CMAKE_CURRENT_BINARY_DIR}/version.rc")

```

在上面的示例中，`version.rc.in` 文件是一个包含版本信息的模板文件，它使用 CMake 变量来填充版本号和其他信息。例如：

```

1 VERSIONINFO
FILEVERSION ${PROJECT_VERSION_MAJOR},${PROJECT_VERSION_MINOR},${PROJECT_VERSION_PATCH},${PROJECT_VERSION_TWEAK}
PRODUCTVERSION ${PROJECT_VERSION_MAJOR},${PROJECT_VERSION_MINOR},${PROJECT_VERSION_PATCH},${PROJECT_VERSION_TWEAK}
BEGIN
  BLOCK "StringFileInfo"
  BEGIN
    BLOCK "040904E4"
    BEGIN
      VALUE "CompanyName", "My Company"
      VALUE "FileDescription", "My Executable"
      VALUE "FileVersion", "${PROJECT_VERSION_MAJOR}.${PROJECT_VERSION_MINOR}.${PROJECT_VERSION_PATCH}.${PROJECT_VERSION_TWEAK}"
      VALUE "InternalName", "MyExecutable"
      VALUE "OriginalFilename", "MyExecutable.exe"
      VALUE "ProductName", "My Product"
      VALUE "ProductVersion", "${PROJECT_VERSION_MAJOR}.${PROJECT_VERSION_MINOR}.${PROJECT_VERSION_PATCH}.${PROJECT_VERSION_TWEAK}"
    END
  END
  BLOCK "VarFileInfo"
  BEGIN
    VALUE "Translation", 0x409, 1252
  END
END

```

在上面的示例中，使用 CMake 变量 `${PROJECT_VERSION_MAJOR}`、`${PROJECT_VERSION_MINOR}`、`${PROJECT_VERSION_PATCH}` 和 `${PROJECT_VERSION_TWEAK}` 来填充版本号和其他信息。您可以根据需要修改这些变量，以便适应您的项目需求。

在 CMake 构建过程中，`configure_file()` 命令将会根据模板文件生成 `version.rc` 文件，并将其添加到可执行文件中。这样，在生成的可执行文件中就会包含版本信息。

请注意，在使用资源文件 (.rc) 时，您需要使用 Visual Studio 或 Windows SDK 中的工具链来编译可执行文件。在使用 CMake 构建过程中，您可以使用 `add_definitions()` 命令来添加必要的编译选项，例如：

```

add_definitions(-DUNICODE -D_UNICODE -DWIN32 -D_WIN32_WINNT=0x0601 -DWINVER=0x0601)

```

这些选项将确保生成的可执行文件与 Windows 平台兼容，并包含必要的资源信息。
```

## 根据文件夹添加 filter 分组

+ [CMake source_group()命令_cmake对源文件分组-CSDN博客 (2024_7_21 16_59_07).html](https://www.yuque.com/attachments/yuque/0/2024/html/22048361/1728630844582-750f8914-2bdd-4f5b-acca-000fa864573d.html)

## gcc, make, cmake

+ **gcc**
编译器，可编译多种语言，但只能编译一个源文件
+ **make**
批处理makefile的工具，执行编译和链接
+ **makefile**
告诉gcc或其他编译器如何编译和链接源文件
+ **cmake**
能生成跨平台的makefile文件给make用
+ **nmake**
vs中的命令，相当于make

## Examples

### Example1

```cmake
cmake_minimum_required(VERSION 3.8)

project(test)

set(DIR1 ${CMAKE_CURRENT_SOURCE_DIR}/src)
set(DIR2 ${CMAKE_CURRENT_SOURCE_DIR}/src/geometry)
set(DIR3 ${CMAKE_CURRENT_SOURCE_DIR}/src/common)

# *.cpp
aux_source_directory(${DIR1} SRCS_PROJ)
aux_source_directory(${DIR2} SRCS_GEOM)
aux_source_directory(${DIR3} SRCS_COMM)
source_group("" FILES ${SRCS_PROJ} ${SRCS_GEOM} ${SRCS_COMM})

# *.h
file(GLOB INCS_PROJ "${DIR1}/*.h")
file(GLOB INCS_GEOM "${DIR2}/*.h")
file(GLOB INCS_COMM "${DIR3}/*.h")

# combine *.h & *.cpp
## combine PROJ
set(PROJ_INCS_SRCS "")
list(APPEND PROJ_INCS_SRCS ${SRCS_PROJ})
list(APPEND PROJ_INCS_SRCS ${INCS_PROJ})
list(LENGTH PROJ_INCS_SRCS PROJ_FILE_NUMS)
message (STATUS ${PROJ_INCS_SRCS})
message (STATUS ${PROJ_FILE_NUMS})
## combine GEOM
set(GEOM_INCS_SRCS "")
list(APPEND GEOM_INCS_SRCS ${SRCS_GEOM})
list(APPEND GEOM_INCS_SRCS ${INCS_GEOM})
list(LENGTH GEOM_INCS_SRCS GEOM_FILE_NUMS)
message (STATUS ${GEOM_INCS_SRCS})
message (STATUS ${GEOM_FILE_NUMS})
## combine COMM
set(COMM_INCS_SRCS "")
list(APPEND COMM_INCS_SRCS ${SRCS_COMM})
list(APPEND COMM_INCS_SRCS ${INCS_COMM})
list(LENGTH COMM_INCS_SRCS COMM_FILE_NUMS)
message (STATUS ${COMM_INCS_SRCS})
message (STATUS ${COMM_FILE_NUMS})

# group
source_group ("" FILES ${PROJ_INCS_SRCS})
source_group (geom FILES ${GEOM_INCS_SRCS})
source_group (comm FILES ${COMM_INCS_SRCS})

# generate dynamic link library
add_library(${CMAKE_PROJECT_NAME} SHARED
${PROJ_INCS_SRCS}
${GEOM_INCS_SRCS}
${COMM_INCS_SRCS}
)
```

### Example2

```cmake
cmake_minimum_required (VERSION 3.24)

project (PolygonsSort)

# .h
include_directories(${CMAKE_CURRENT_SOURCE_DIR}/src
${CMAKE_CURRENT_SOURCE_DIR}/src/common
${CMAKE_CURRENT_SOURCE_DIR}/src/geometry)

set(PROJ_INCS
"./src/polygons_sort_interface.h"
"./src/ps_polygons_sort.h"
"./src/ps_read.h"
)

set(COMMON_INCS
"./src/common/common.h"
"./src/common/declare.h"
"./src/common/fitline.h"
)

set(GEOMETRY_INCS
"./src/geometry/geometry.h"
"./src/geometry/ps_polygon.h"
"./src/geometry/ps_rect.h"
)

source_group("" FILES ${PROJ_INCS})
source_group(common FILES ${COMMON_INCS})
source_group(geometry FILES ${GEOMETRY_INCS})

message(STATUS ${PROJ_INCS})
message(STATUS ${COMMON_INCS})
message(STATUS ${GEOMETRY_INCS})

# .cpp
aux_source_directory(./src PROJ_SRCS)
aux_source_directory(./src/common COMMON_SRCS)
aux_source_directory(./src/geometry GEOMETRY_SRCS)

add_library(${PROJECT_NAME} SHARED
${PROJ_SRCS} ${COMMON_SRCS} ${GEOMETRY_SRCS}
${PROJ_INCS} ${COMMON_INCS} ${GEOMETRY_INCS}
)

```

### Example3

```git
cmake_minimum_required(VERSION 3.12)

project(MathOperations VERSION 1.0.0)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED True)

set(CMAKE_DEBUG_POSTFIX "_debug")
set(CMAKE_RELEASE_POSTFIX "_release")

file(GLOB_RECURSE SRC_FILES "src/*.h" "src/*.cpp")

add_library(${PROJECT_NAME} SHARED
    ${SRC_FILES}
)
target_compile_definitions(${PROJECT_NAME}
    PRIVATE "DLL_EXPORT" "_CRT_SECURE_NO_WARNINGS"
)

target_include_directories(${PROJECT_NAME}
    INTERFACE
    $<INSTALL_INTERFACE:include>
)

install(TARGETS ${PROJECT_NAME}
    EXPORT ${PROJECT_NAME}Targets
    LIBRARY DESTINATION libS
    ARCHIVE DESTINATION libS
    RUNTIME DESTINATION binS
)

install(DIRECTORY include
    DESTINATION include
)

install(EXPORT ${PROJECT_NAME}Targets
    FILE ${PROJECT_NAME}Targets.cmake
    DESTINATION "share/cmake"
)

# include(InstallRequiredSystemLibraries)
set(CPACK_PACKAGE_VERSION ${PROJECT_VERSION})
set(CPACK_GENERATOR ZIP)
set(CPACK_OUTPUT_FILE_PREFIX "../upload")
include(CPACK)
```

## Sources

1. [cmake-demo-master.zip]()
2. [CMakeTutorial-master.zip]()
3. [learning-cmake-master.zip]()
4. [cmake-examples-master.zip]()
5. [cmake_template-main.zip]()
