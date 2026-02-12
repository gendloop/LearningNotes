# Tutorial

## About

This provides a step-by-step guide that covers common build system issues.

## Steps

### Step1: A Basic Starting Point

#### 1.1 Basic

**treeview**

```markdown
1.1/
├── src/
│   └── tutorials.cxx
└── CMakeLists.txt
```

**CMakeLists.txt**

```cmake
cmake_minimum_required(VERSION 3.10)

# set the <project name>
project(Tutorials)

# add the executable
add_executable(Tutorial src/tutorials.cxx)
```

#### 1.2 Add a Version Number and Configured Header File

**treeview**

```markdown
1.2/
├── src/
│   └── tutorials.cxx
├── CMakeLists.txt
└── TutorialConfig.h.in
```

**CMakeLists.txt**

```cmake
cmake_minimum_required(VERSION 3.10)

# set the <project name>
# project(Tutorials)

# set the <project name> and <version>
project(Tutorials VERSION 1.0)

configure_file(TutorialConfig.h.in TutorialConfig.h)

add_executable(Tutorial src/tutorials.cxx)

target_include_directories(Tutorial PUBLIC
  "${PROJECT_BINARY_DIR}"
)
```

#### 1.3 Specify the C Standard

**treeview**

```markdown
1.3/
├── src/
│   └── tutorials.cxx
├── CMakeLists.txt
└── TutorialConfig.h.in
```

**CMakeLists**

```cmake
cmake_minimum_required(VERSION 3.10)

# set the <project name> and <version>
project(Tutorials VERSION 1.0)

# specify the C++ standard
set(CMAKE_CXX_STANDARD 14)
set(CMAKE_CXX_STANDARD_REQUIRED True)

configure_file(TutorialConfig.h.in TutorialConfig.h)

add_executable(Tutorial src/tutorials.cxx)

target_include_directories(Tutorial PUBLIC
  "${PROJECT_BINARY_DIR}"
)
```

### Step2: Adding a Library

#### 2.1 Add a Static Library

**treeview**

```markdown
2.1/
├── 3rdParty/
│   └── MathFunctions/
│       ├── CMakeLists.txt
│       ├── MathFunctions.h
│       └── mysqrt.cxx
├── src/
│   └── main.cpp
├── CMakeLists.txt
└── Config.h.in
```

**MathFunctions/CMakeLists.txt**

```cmake
add_library(MathFunctions mysqrt.cxx)
```

**CMakeLists.txt**

```cmake
# cmake version
cmake_minimum_required(VERSION 3.10)

# project
project(Step2Project VERSION 2.0)

# c++ standard
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED True)

# config file
configure_file(Config.h.in config.h)

# 3rdParty
add_subdirectory(3rdParty/MathFunctions)

# target
add_executable(Step2 src/main.cpp)

# target link
target_link_libraries(Step2 PUBLIC
  MathFunctions
)

# target include
target_include_directories(Step2 PUBLIC
  "${PROJECT_BINARY_DIR}"
  "${PROJECT_SOURCE_DIR}/3rdParty/MathFunctions"
)
```

#### 2.2 Add an Optional Staic Library

**treeview**

```markdown
2.2/
├── 3rdParty/
│   └── MathFunctions/
│       ├── CMakeLists.txt
│       ├── MathFunctions.h
│       └── mysqrt.cxx
├── src/
│   └── main.cpp
├── CMakeLists.txt
└── Config.h.in
```

**MathFunctions/CMakeLists.txt**

```cmake
add_library(MathFunctions mysqrt.cxx)
```

**CMakeLists.txt**

```cmake
# cmake version
cmake_minimum_required(VERSION 3.10)

# project
project(Step2Project VERSION 2.0)

# c++ standard
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED, True)

# define variables
option(USE_MATH "Use my math functions" ON)

# config file
configure_file(Config.h.in config.h)

# 3rdParty
if(USE_MATH)
    add_subdirectory(3rdParty/MathFunctions)
    list(APPEND EXTRA_LIBS MathFunctions)
    list(APPEND EXTRA_INCLUDES "${PROJECT_SOURCE_DIR}/3rdParty/MathFunctions")
endif()

# target
add_executable(Step2 src/main.cpp)

# target link
target_link_libraries(Step2 PUBLIC
  ${EXTRA_LIBS}
)

# target include
target_include_directories(Step2 PUBLIC
  "${PROJECT_BINARY_DIR}"
  ${EXTRA_INCLUDES}
)
```

### Step3: Adding Usage Requirements for a Library

**treeview**

```markdown
Step3/
├── 3rdParty/
│   └── MathFunctions/
│       ├── CMakeLists.txt
│       ├── MathFunctions.h
│       └── mysqrt.cxx
├── src/
│   └── main.cpp
├── CMakeLists.txt
└── Config.h.in
```

**MathFunctions/CMakeLists.txt**

```cmake
add_library(MathFunctions
  mysqrt.cxx
)
target_include_directories(MathFunctions
  INTERFACE
  ${CMAKE_CURRENT_SOURCE_DIR}
)
```

**CMakeLists.txt**

```cmake
# cmake version
cmake_minimum_required(VERSION 3.10)

# project
project(Step2Project VERSION 2.0)

# c++ standard
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED, True)

# define variables
option(USE_MATH "Use my math functions" ON)

# config file
configure_file(Config.h.in config.h)

# 3rdParty
if(USE_MATH)
    add_subdirectory(3rdParty/MathFunctions)
    list(APPEND EXTRA_LIBS MathFunctions)
endif()

# target
add_executable(Step2 src/main.cpp)

# target link
target_link_libraries(Step2 PUBLIC
                    ${EXTRA_LIBS}
)

# target include
target_include_directories(Step2 PUBLIC
                        "${PROJECT_BINARY_DIR}"
)
```

### Step4: Installing and Testing

#### 4.1 Installing

**treeview**

```markdown
4.1/
├── 3rdParty/
│   └── MathFunctions/
│       ├── CMakeLists.txt
│       ├── MathFunctions.h
│       └── mysqrt.cxx
├── src/
│   └── main.cpp
├── CMakeLists.txt
└── Config.h.in
```

**MathFunctions/CMakeLists.txt**

```cmake
add_library(MathFunctions
  mysqrt.cxx
)
target_include_directories(MathFunctions
  INTERFACE
  ${CMAKE_CURRENT_SOURCE_DIR}
)

# install
install(TARGETS MathFunctions DESTINATION lib)
install(FILES MathFunctions.h DESTINATION include/MathFunctions)
```

**CMakeLists.txt**

```cmake
# cmake version
cmake_minimum_required(VERSION 3.10)

# project
project(Step2Project VERSION 2.0)

# c++ standard
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED, True)

# define variables
option(USE_MATH "Use my math functions" ON)

# config file
configure_file(Config.h.in config.h)

# 3rdParty
if(USE_MATH)
  add_subdirectory(3rdParty/MathFunctions)
  list(APPEND EXTRA_LIBS MathFunctions)
endif()

# target
add_executable(Step2 src/main.cpp)

# target link
target_link_libraries(Step2 PUBLIC
  ${EXTRA_LIBS}
)

# target include
target_include_directories(Step2 PUBLIC
  "${PROJECT_BINARY_DIR}"
)

# install
install(TARGETS Step2 DESTINATION bin)
install(FILES "${PROJECT_BINARY_DIR}/config.h"
  DESTINATION include
)
```

**Commands**

1. `cmake --build . --config Release`
2. `cmake --install . --prefix ./install`

#### 4.2 Testing

**treeview**

```markdown
4.2/
├── 3rdParty/
│   └── MathFunctions/
│       ├── CMakeLists.txt
│       ├── MathFunctions.h
│       └── mysqrt.cxx
├── src/
│   └── main.cpp
├── CMakeLists.txt
└── Config.h.in
```

**MathFunctions/CMakeLists.txt**

```cmake
add_library(MathFunctions
            mysqrt.cxx
            )
target_include_directories(MathFunctions
                        INTERFACE
                        ${CMAKE_CURRENT_SOURCE_DIR}
                        )
install(TARGETS MathFunctions DESTINATION lib)
install(FILES MathFunctions.h DESTINATION include/MathFunctions)
```

**CMakeLists.txt**

```cmake
cmake_minimum_required(VERSION 3.10)
project(Step2Project VERSION 2.0)
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED True)
option(USE_MATH "Use my math functions" ON)
configure_file(Config.h.in config.h)
if(USE_MATH)
    add_subdirectory(3rdParty/MathFunctions)
    list(APPEND EXTRA_LIBS MathFunctions)
endif()
add_executable(Step2 src/main.cpp)
target_link_libraries(Step2 PUBLIC
                    ${EXTRA_LIBS}
)
target_include_directories(Step2 PUBLIC
                        "${PROJECT_BINARY_DIR}"
)
install(TARGETS Step2 DESTINATION bin)
install(FILES "${PROJECT_BINARY_DIR}/config.h"
    DESTINATION include
    )
enable_testing()
# Basic form: dose the application run
add_test(NAME RUN COMMAND Step2 9)
# does the usage message work
add_test(NAME Usage COMMAND Step2)
set_tests_properties(Usage
    PROPERTIES PASS_REGULAR_EXPRESSION "VERSION_MAJOR: .*"
)
# define a function to simplifiy adding tests
function(do_test target arg result)
    add_test(NAME Comp${arg} COMMAND ${target} ${arg})
    set_tests_properties(Comp${arg}
        PROPERTIES PASS_REGULAR_EXPRESSION ${result}
    )
endfunction()
# do a bunch of result based tests
do_test(Step2 4 "sqrt value: 2")
do_test(Step2 9 "sqrt value: 3")
do_test(Step2 15 "sqrt value: 3.9")
```

### Step5: Adding System Introspection

#### 5.1 Testing the Availability of Functions

**treeview**

```markdown
5.1/
├── 3rdParty/
│   └── MathFunctions/
│       ├── CMakeLists.txt
│       ├── MathFunctions.h
│       └── mysqrt.cxx
├── src/
│   └── main.cpp
├── CMakeLists.txt
└── Config.h.in
```

**MathFunctions/CMakeLists.txt**

```cmake
add_library(MathFunctions
            mysqrt.cxx
            )
target_include_directories(MathFunctions
                        INTERFACE
                        ${CMAKE_CURRENT_SOURCE_DIR}
                        )
# does this system provide the log and exp func ?
include(CheckCXXSourceCompiles)
check_cxx_source_compiles("
    #include <cmath>
    int main() {
        std::log(1.0);
        return 0;
    }
" HAVE_LOG)
check_cxx_source_compiles("
    #include <cmath>
    int main() {
        std::exp(1.0);
        return 0;
    }
" HAVE_EXP)

if(HAVE_LOG AND HAVE_EXP)
    target_compile_definitions(MathFunctions
        PRIVATE "HAVE_LOG" "HAVE_EXP"
    )
endif()

# install
install(TARGETS MathFunctions DESTINATION lib)
install(FILES MathFunctions.h DESTINATION include/MathFunctions)
```

**CMakeLists.txt**

```cmake
cmake_minimum_required(VERSION 3.10)
project(Step2Project VERSION 2.0)
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED True)
# define variables
option(USE_MATH "Use my math functions" ON)
# config file
configure_file(Config.h.in config.h)
# 3rdParty
if(USE_MATH)
    add_subdirectory(3rdParty/MathFunctions)
    list(APPEND EXTRA_LIBS MathFunctions)
endif()
# target
add_executable(Step2 src/main.cpp)
# target link
target_link_libraries(Step2 PUBLIC
                    ${EXTRA_LIBS}
)
# target include
target_include_directories(Step2 PUBLIC
                        "${PROJECT_BINARY_DIR}"
)
#install
install(TARGETS Step2 DESTINATION bin)
install(FILES "${PROJECT_BINARY_DIR}/config.h"
    DESTINATION include
    )
enable_testing()
# Basic form: dose the application run
add_test(NAME RUN COMMAND Step2 9)
```

#### 5.2 Testing PUBLIC | PRIVATE | INTERFACE

* `PUBLIC`  I have, and so do you.
* `PRIVATE` I have, but you don't.
* `INTERFACE` I don't, but you have.

### Step6: Adding a Custom Command and Generated File

#### 6.1 Adding a Custom Command in subproject

**treeview**

```markdown
6.1/
├── 3rdParty/
│   └── MathFunctions/
│       ├── CMakeLists.txt
│       ├── MakeTable.cpp
│       ├── MathFunctions.h
│       └── mysqrt.cxx
├── src/
│   └── main.cpp
├── CMakeLists.txt
└── Config.h.in
```

**MathFunctions/CMakeLists.txt**

```cmake
add_executable(MakeTable MakeTable.cpp)

# how to produce 'Table.h'
add_custom_command(
    OUTPUT ${CMAKE_CURRENT_BINARY_DIR}/Table.h
    COMMAND MakeTable ${CMAKE_CURRENT_BINARY_DIR}/Table.h
    DEPENDS MakeTable
)

add_library(MathFunctions
            mysqrt.cxx
            ${CMAKE_CURRENT_BINARY_DIR}/Table.h
)

target_include_directories(MathFunctions
    INTERFACE ${CMAKE_CURRENT_SOURCE_DIR}
    PRIVATE ${CMAKE_CURRENT_BINARY_DIR}
)

# install
install(TARGETS MathFunctions DESTINATION lib)
install(FILES MathFunctions.h DESTINATION include/MathFunctions)
```

**CMakeLists.txt**

```cmake
# cmake version
cmake_minimum_required(VERSION 3.10)

# project
project(Step2Project VERSION 2.0)

# c standard
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED True)

# define variables
option(USE_MATH "Use my math functions" ON)

# config file
configure_file(Config.h.in config.h)

# 3rdParty
if(USE_MATH)
    add_subdirectory(3rdParty/MathFunctions)
    list(APPEND EXTRA_LIBS MathFunctions)
endif()

# target
add_executable(Step2 src/main.cpp)

# target link
target_link_libraries(Step2 PUBLIC
                    ${EXTRA_LIBS}
)

# target include
target_include_directories(Step2 PUBLIC
                        "${PROJECT_BINARY_DIR}"
)

#install
install(TARGETS Step2 DESTINATION bin)
install(FILES "${PROJECT_BINARY_DIR}/config.h"
    DESTINATION include
    )

enable_testing()

# Basic form: dose the application run
add_test(
    NAME test1
    COMMAND Step2
)
add_test(
    NAME test2
    COMMAND Step2 2
)

```

#### 6.2 Adding a Custom Command in main project

**treeview**

```markdown
6.2/
├── 3rdParty/
│   └── MathFunctions/
│       ├── CMakeLists.txt
│       ├── MathFunctions.h
│       └── mysqrt.cxx
├── src/
│   └── main.cpp
├── CMakeLists.txt
├── Config.h.in
└── MakeTable.cpp
```

**MathFuncions/CMakeLists.txt**

```cmake
add_library(MathFunctions
            mysqrt.cxx
)

target_include_directories(MathFunctions
    INTERFACE ${CMAKE_CURRENT_SOURCE_DIR}
)

# install
install(TARGETS MathFunctions DESTINATION lib)
install(FILES MathFunctions.h DESTINATION include/MathFunctions)
```

**CMakeLists.txt**

```cmake
# cmake version
cmake_minimum_required(VERSION 3.10)

# project
project(Step2Project VERSION 2.0)

# c standard
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED True)

# define variables
option(USE_MATH "Use my math functions" ON)

# config file
configure_file(Config.h.in config.h)

# generate MakeATable.exe
add_executable(MakeATable MakeTable.cpp)

# adding custom command
add_custom_command(
    OUTPUT ${PROJECT_SOURCE_DIR}/src/a_table.h
    COMMAND MakeATable ${PROJECT_SOURCE_DIR}/src/a_table.h
    DEPENDS MakeATable
)

# 3rdParty
if(USE_MATH)
    add_subdirectory(3rdParty/MathFunctions)
    list(APPEND EXTRA_LIBS MathFunctions)
endif()

# target
add_executable(Step2
    src/main.cpp
    ${PROJECT_SOURCE_DIR}/src/a_table.h
)

# target link
target_link_libraries(Step2 PUBLIC
                    ${EXTRA_LIBS}
)

# target include
target_include_directories(Step2 PUBLIC
                        "${PROJECT_BINARY_DIR}"
                        "${PROJECT_SOURCE_DIR}/src"
)

#install
install(TARGETS Step2 DESTINATION bin)
install(FILES "${PROJECT_BINARY_DIR}/config.h"
    DESTINATION include
    )

enable_testing()

# Basic form: dose the application run
add_test(
    NAME test1
    COMMAND Step2 2
)
add_test(
    NAME test2
    COMMAND Step2 4
)
add_test(
    NAME test3
    COMMAND Step2 6
)
```

### Step7: Packing an Installer

#### 7.1 Packing an installer for an interface library

**treeview**

```markdown
7.1/
├── 3rdParty/
│   └── MathFunctions/
│       ├── CMakeLists.txt
│       ├── MathFunctions.h
│       └── mysqrt.cxx
├── src/
│   ├── a_table.h
│   └── main.cpp
├── CMakeLists.txt
├── Config.h.in
├── License.txt
└── MakeTable.cpp
```

**MathFunctions/CMakeLists.txt**

```cmake
add_library(MathFunctions
            mysqrt.cxx
)

target_include_directories(MathFunctions
    INTERFACE ${CMAKE_CURRENT_SOURCE_DIR}
)

# install
# install(TARGETS MathFunctions
#     DESTINATION lib
# )
# install(FILES MathFunctions.h
#     DESTINATION include/MathFunctions
# )
```

**CMakeLists.txt**

```cmake
# cmake version
cmake_minimum_required(VERSION 3.10)

# project
project(Step2Project VERSION 2.0.1)

# c standard
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED True)

# define variables
option(USE_MATH "Use my math functions" ON)

# config file
configure_file(Config.h.in config.h)

# generate MakeATable.exe
add_executable(MakeATable MakeTable.cpp)

# adding custom command
add_custom_command(
    OUTPUT ${PROJECT_SOURCE_DIR}/src/a_table.h
    COMMAND MakeATable ${PROJECT_SOURCE_DIR}/src/a_table.h
    DEPENDS MakeATable
)

# 3rdParty
if(USE_MATH)
    add_subdirectory(3rdParty/MathFunctions)
    list(APPEND EXTRA_LIBS MathFunctions)
endif()

# target
add_executable(Step2
    src/main.cpp
    ${PROJECT_SOURCE_DIR}/src/a_table.h
)

# target link
target_link_libraries(Step2 PRIVATE
                    ${EXTRA_LIBS}
)

# target include
target_include_directories(Step2 PRIVATE
                        "${PROJECT_BINARY_DIR}"
                        "${PROJECT_SOURCE_DIR}/src"
)

#install
install(TARGETS Step2
    DESTINATION bin
)
install(FILES "${PROJECT_BINARY_DIR}/config.h"
    DESTINATION include
)

enable_testing()

# Basic form: dose the application run
add_test(
    NAME test1
    COMMAND Step2 2
)
add_test(
    NAME test2
    COMMAND Step2 4
)
add_test(
    NAME test3
    COMMAND Step2 6
)

# include runtime module
# include(InstallRequiredSystemLibraries)

# set some CPACK variables
set(CPACK_RESOURCE_FILE_LICENSE "${CMAKE_CURRENT_SOURCE_DIR}/License.txt")
set(CPACK_PACKAGE_VERSION_MAJOR "${Step2Project_VERSION_MAJOR}")
set(CPACK_PACKAGE_VERSION_MINOR "${Step2Project_VERSION_MINOR}")
set(CPACK_PACKAGE_VERSION_MINOR "${Step2Project_VERSION_PATCH}")
set(CPACK_SOURCE_GENERATOR "TAG")

# include CPACK module
include(CPACK)
```

### Step8: /

### Step9: Selecting Static or Shared Libraries

#### 9.1 Selecting Shared Libraries

**treeview**

```markdown
9.1/
├── 3rdParty/
│   └── MathFunctions/
│       ├── MyAdd/
│       │   ├── my_add.cpp
│       │   └── my_add.h
│       ├── MySqrt/
│       │   ├── my_sqrt.cpp
│       │   └── my_sqrt.h
│       ├── CMakeLists.txt
│       ├── math_functions.cpp
│       └── math_functions.h
├── src/
│   └── main.cpp
├── CMakeLists.txt
└── config.h.in
```

**MathFunctions/CMakeLists.txt**

```cmake
option(USE_MYMATH "Use my math" ON)

#  MathFunctions
add_library(MathFunctions SHARED
    math_functions.h
    math_functions.cpp
)
target_include_directories(MathFunctions INTERFACE ${CMAKE_CURRENT_SOURCE_DIR})
target_compile_definitions(MathFunctions PRIVATE "USE_MYMATH")
target_compile_definitions(MathFunctions PRIVATE "EXPORTING_MYMATH")

if(USE_MYMATH)
    # MySqrt
    add_library(MySqrt SHARED
        MySqrt/my_sqrt.h
        MySqrt/my_sqrt.cpp
    )
    target_compile_definitions(MySqrt PRIVATE "EXPORTING_MYSQRT")
    target_include_directories(MySqrt INTERFACE ${CMAKE_CURRENT_SOURCE_DIR}/MySqrt)

    # MyAdd
    add_library(MyAdd SHARED
        MyAdd/my_add.h
        MyAdd/my_add.cpp
    )
    target_compile_definitions(MyAdd PRIVATE "EXPORTING_MYADD")
    target_include_directories(MyAdd INTERFACE ${CMAKE_CURRENT_SOURCE_DIR}/MyAdd)

    target_link_libraries(MathFunctions PRIVATE MySqrt)
    target_link_libraries(MathFunctions PRIVATE MyAdd)
endif()


set(installable_libs MathFunctions)
if(TARGET MySqrt)
    list(APPEND installable_libs MySqrt)
endif()
if(TARGET MyAdd)
    list(APPEND installable_libs MyAdd)
endif()

install(TARGETS ${installable_libs}
    RUNTIME DESTINATION bin
)
install(TARGETS MathFunctions
    LIBRARY DESTINATION lib
)
install(FILES math_functions.h
    DESTINATION include
)
```

**CMakeLists.txt**

```cmake
cmake_minimum_required(VERSION 3.10)

project(Step9 VERSION 1.9.1)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIED True)

set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY "${PROJECT_BINARY_DIR}")
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY "${PROJECT_BINARY_DIR}")
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY "${PROJECT_BINARY_DIR}")

configure_file(config.h.in config.h)

add_subdirectory(3rdParty/MathFunctions)

add_executable(Step9 src/main.cpp)
target_include_directories(Step9 PRIVATE ${CMAKE_BINARY_DIR})
target_link_libraries(Step9 PUBLIC MathFunctions)

include(CTest)
add_test(NAME Runs COMMAND Step9 25)
set_tests_properties(Runs
    PROPERTIES PASS_REGULAR_EXPRESSION "The square root of [0-9 is [0-9]+"
)

function(do_sqr_test target arg result)
    add_test(NAME Sqr${arg}
        COMMAND ${target} ${arg}
    )
    set_tests_properties(Sqr${arg}
        PROPERTIES PASS_REGULAR_EXPRESSION ${result}
    )
endfunction()

do_sqr_test(Step9 4 "The square root of 4 is 2")
do_sqr_test(Step9 9 "The square root of 9 is 3")

function(do_add_test target x y ret)
    add_test(NAME Add${x}-${y}
        COMMAND ${target} ${x} ${y}
    )
    set_tests_properties(Add${x}-${y}
        PROPERTIES PASS_REGULAR_EXPRESSION ${ret}
    )
endfunction()

do_add_test(Step9 1 2 "The add result of [0-9. and [0-9. is [0-9.]+")
do_add_test(Step9 2 4 "The add result of [0-9. and [0-9. is [0-9.]+")
```

#### 9.2 Selecting Static Libraries

**treeview**

```markdown
9.2/
├── 3rdParty/
│   └── MathFunctions/
│       ├── MyAdd/
│       │   ├── my_add.cpp
│       │   └── my_add.h
│       ├── MySqrt/
│       │   ├── my_sqrt.cpp
│       │   └── my_sqrt.h
│       ├── CMakeLists.txt
│       ├── math_functions.cpp
│       └── math_functions.h
├── src/
│   └── main.cpp
├── CMakeLists.txt
└── config.h.in
```

**MathFunctions/CMakeLists.txt**

```cmake
option(USE_MYMATH "Use my math" OFF)

#  MathFunctions
add_library(MathFunctions STATIC
    math_functions.h
    math_functions.cpp
)
target_include_directories(MathFunctions INTERFACE ${CMAKE_CURRENT_SOURCE_DIR})

if(USE_MYMATH)
    # MathFunctions
    target_compile_definitions(MathFunctions PRIVATE "USE_MYMATH")

    # MySqrt
    add_library(MySqrt STATIC
        MySqrt/my_sqrt.h
        MySqrt/my_sqrt.cpp
    )
    target_include_directories(MySqrt INTERFACE ${CMAKE_CURRENT_SOURCE_DIR}/MySqrt)

    # MyAdd
    add_library(MyAdd STATIC
        MyAdd/my_add.h
        MyAdd/my_add.cpp
    )
    target_include_directories(MyAdd INTERFACE ${CMAKE_CURRENT_SOURCE_DIR}/MyAdd)

    target_link_libraries(MathFunctions PRIVATE MySqrt)
    target_link_libraries(MathFunctions PRIVATE MyAdd)
endif()


set(installable_libs MathFunctions)

if(TARGET MySqrt)
    list(APPEND installable_libs MySqrt)
endif()

if(TARGET MyAdd)
    list(APPEND installable_libs MyAdd)
endif()

install(TARGETS ${installable_libs}
    LIBRARY DESTINATION lib
)
install(FILES math_functions.h
    DESTINATION include
)
```

**CMakeLitsts.txt**

```cmake
cmake_minimum_required(VERSION 3.10)

project(Step9 VERSION 1.9.2)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIED True)

set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY "${PROJECT_BINARY_DIR}")
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY "${PROJECT_BINARY_DIR}")
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY "${PROJECT_BINARY_DIR}")

configure_file(config.h.in config.h)

add_subdirectory(3rdParty/MathFunctions)

add_executable(Step9 src/main.cpp)
target_include_directories(Step9 PRIVATE ${CMAKE_BINARY_DIR})
target_link_libraries(Step9 PUBLIC MathFunctions)

include(CTest)
add_test(NAME Runs COMMAND Step9)
set_tests_properties(Runs
    PROPERTIES PASS_REGULAR_EXPRESSION ".*[0-9]+\.[0-9]+\.[0-9]+"
)

function(do_sqr_test target arg result)
    add_test(NAME Sqr${arg}
        COMMAND ${target} ${arg}
    )
    set_tests_properties(Sqr${arg}
        PROPERTIES PASS_REGULAR_EXPRESSION ${result}
    )
endfunction()

do_sqr_test(Step9 4 "The square root of 4 is 2")
do_sqr_test(Step9 9 "The square root of 9 is 3")

function(do_add_test target x y ret)
    add_test(NAME Add${x}-${y}
        COMMAND ${target} ${x} ${y}
    )
    set_tests_properties(Add${x}-${y}
        PROPERTIES PASS_REGULAR_EXPRESSION ${ret}
    )
endfunction()

do_add_test(Step9 1 2 "The add result of [0-9. and [0-9. is [0-9.]+")
do_add_test(Step9 2 4 "The add result of [0-9. and [0-9. is [0-9.]+")
```

### Step10: Adding Generator Expressions /

### Step11: Adding Export Configuration

#### 11.1 Export

**treeview**

```markdown
11.1/
├── 3rdParty/
│   └── MathFunctions/
│       ├── MyAdd/
│       │   ├── my_add.cpp
│       │   └── my_add.h
│       ├── MySqrt/
│       │   ├── my_sqrt.cpp
│       │   └── my_sqrt.h
│       ├── CMakeLists.txt
│       ├── math_functions.cpp
│       └── math_functions.h
├── src/
│   └── main.cpp
├── CMakeLists.txt
├── config.cmake.in
└── config.h.in
```

**MathFunctions/CMakeLists.txt**

```cmake
option(USE_MYMATH "Use my math" OFF)

#  MathFunctions
add_library(MathFunctions STATIC
    math_functions.h
    math_functions.cpp
)
target_include_directories(MathFunctions INTERFACE ${CMAKE_CURRENT_SOURCE_DIR})

if(USE_MYMATH)
    # MathFunctions
    target_compile_definitions(MathFunctions PRIVATE "USE_MYMATH")

    # MySqrt
    add_library(MySqrt STATIC
        MySqrt/my_sqrt.h
        MySqrt/my_sqrt.cpp
    )
    target_include_directories(MySqrt INTERFACE ${CMAKE_CURRENT_SOURCE_DIR}/MySqrt)

    # MyAdd
    add_library(MyAdd STATIC
        MyAdd/my_add.h
        MyAdd/my_add.cpp
    )
    target_include_directories(MyAdd INTERFACE ${CMAKE_CURRENT_SOURCE_DIR}/MyAdd)

    target_link_libraries(MathFunctions PRIVATE MySqrt)
    target_link_libraries(MathFunctions PRIVATE MyAdd)
endif()


set(installable_libs MathFunctions)

if(TARGET MySqrt)
    list(APPEND installable_libs MySqrt)
endif()

if(TARGET MyAdd)
    list(APPEND installable_libs MyAdd)
endif()

install(TARGETS ${installable_libs}
    LIBRARY DESTINATION lib
)
install(FILES math_functions.h
    DESTINATION include
)

```

**CMakeLists.txt**

```cmake
cmake_minimum_required(VERSION 3.10)

project(Step9 VERSION 1.9.2)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIED True)

set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY "${PROJECT_BINARY_DIR}")
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY "${PROJECT_BINARY_DIR}")
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY "${PROJECT_BINARY_DIR}")

configure_file(config.h.in config.h)

add_subdirectory(3rdParty/MathFunctions)

add_executable(Step9 src/main.cpp)
target_include_directories(Step9 PRIVATE ${CMAKE_BINARY_DIR})
target_link_libraries(Step9 PUBLIC MathFunctions)

install(EXPORT MathFunctionsTargets
    FILE MathFunctionsTargets.cmake
    # NAMESPACE ${PROJECT_NAME}::
    DESTINATION lib/cmake/MathFunctions
)

include(CMakePackageConfigHelpers)
configure_package_config_file(
    ${PROJECT_SOURCE_DIR}/config.cmake.in
    ${PROJECT_BINARY_DIR}/MathFunctionsConfig.cmake
    INSTALL_DESTINATION lib/cmake/MathFunctions
    NO_SET_AND_CHECK_MACRO
    NO_CHECK_REQUIRED_COMPONENTS_MACRO
)

write_basic_package_version_file(
    "${CMAKE_CURRENT_BINARY_DIR}/MathFunctionsConfigVersion.cmake"
    VERSION "${${PROJECT_NAME}_VERSION_MAJOR}.${${PROJECT_NAME}_VERSION_MINOR}.${${PROJECT_NAME}_VERSION_PATCH}"
    COMPATIBILITY AnyNewerVersion
)

install(FILES
    ${CMAKE_CURRENT_BINARY_DIR}/MathFunctionsConfig.cmake
    ${CMAKE_CURRENT_BINARY_DIR}/MathFunctionsConfigVersion.cmake
    DESTINATION lib/cmake/MathFunctions
)

export(EXPORT MathFunctionsTargets
    FILE "${CMAKE_CURRENT_BINARY_DIR}/MathFunctionsTargets.cmake"
)

include(CTest)
add_test(NAME Runs COMMAND Step9)
set_tests_properties(Runs
    PROPERTIES PASS_REGULAR_EXPRESSION ".*[0-9]+\.[0-9]+\.[0-9]+"
)

function(do_sqr_test target arg result)
    add_test(NAME Sqr${arg}
        COMMAND ${target} ${arg}
    )
    set_tests_properties(Sqr${arg}
        PROPERTIES PASS_REGULAR_EXPRESSION ${result}
    )
endfunction()

do_sqr_test(Step9 4 "The square root of 4 is 2")
do_sqr_test(Step9 9 "The square root of 9 is 3")

function(do_add_test target x y ret)
    add_test(NAME Add${x}-${y}
        COMMAND ${target} ${x} ${y}
    )
    set_tests_properties(Add${x}-${y}
        PROPERTIES PASS_REGULAR_EXPRESSION ${ret}
    )
endfunction()

do_add_test(Step9 1 2 "The add result of [0-9. and [0-9. is [0-9.]+")
do_add_test(Step9 2 4 "The add result of [0-9. and [0-9. is [0-9.]+")
```

#### 11.2 Import a package

> build: 11.1 => static library and export without namespace

[find_package](https://cmake.org/cmake/help/v3.24/command/find_package.html?highlight=find_package)

**treeview**

```markdown
11.2/
├── src/
│   └── main.cpp
└── CMakeLists.txt
```

**CMakeLists.txt**

```cmake
cmake_minimum_required(VERSION 3.10)

set(MathFunctions_DIR "../11.1/build/install/lib/cmake/MathFunctions")

find_package(MathFunctions CONFIG REQUIRED)

project(TestStep9 VERSION 1.9.2)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED True)

if(MathFunctions_FOUND)
 add_executable(${PROJECT_NAME} src/main.cpp)

 target_link_libraries(TestStep9 PRIVATE MathFunctions)

 include(CTest)
 add_test(NAME T1 COMMAND TestStep9)
endif()
```

#### 11.3 Import a package with NAMESPACE

> build: 11.1 => static library and export with namespace

**CMakeLists.txt**

```cmake
cmake_minimum_required(VERSION 3.10)

set(MathFunctions_DIR "../11.1/build/install/lib/cmake/MathFunctions")

find_package(MathFunctions CONFIG REQUIRED)

project(TestStep9 VERSION 1.9.2)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED True)

if(MathFunctions_FOUND)
 add_executable(${PROJECT_NAME} src/main.cpp)

 target_link_libraries(TestStep9 PRIVATE Step9::MathFunctions)

 include(CTest)
 add_test(NAME T1 COMMAND TestStep9)
endif()
```

#### 11.4 Import a package with COMPONENTS

> build: 11.1 => static library and export with namespace

**CMakeLists.txt**

```cmake
cmake_minimum_required(VERSION 3.10)

set(MathFunctions_DIR "../11.1/build/install/lib/cmake/MathFunctions")

find_package(MathFunctions CONFIG
 REQUIRED COMPONENTS Step9::MyAdd
)

project(TestStep9 VERSION 1.9.2)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED True)

if(MathFunctions_FOUND)
 add_executable(${PROJECT_NAME} src/main.cpp)

 target_link_libraries(TestStep9 PRIVATE Step9::MyAdd)

 include(CTest)
 add_test(NAME T1 COMMAND TestStep9)
endif()
```

#### 11.5 Import a shared library

> build: 11.1 => dynamic library and export with namespace

**CMakeLists.txt**

```cmake
cmake_minimum_required(VERSION 3.10)

set(MathFunctions_PATH "${CMAKE_CURRENT_SOURCE_DIR}/../11.1/build/install")

project(TestStep9 VERSION 1.9.2)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED True)

add_executable(${PROJECT_NAME} src/main.cpp)

target_include_directories(TestStep9 PRIVATE ${MathFunctions_PATH}/include)
target_link_libraries(TestStep9 PRIVATE ${MathFunctions_PATH}/lib/MathFunctions.lib)

set(CMAKE_RUNTIME_OUTPUT_DIRECTORY "${PROJECT_BINARY_DIR}")
file(COPY "${MathFunctions_PATH}/bin/MathFunctions.dll" DESTINATION "${PROJECT_BINARY_DIR}/Debug")

include(CTest)
add_test(NAME T1 COMMAND TestStep9)
```

### Step12: Packaging Debug and Release

#### 12.1 Packaging Debug and Release

**treeview**

```markdown
12.1/
├── 3rdParty/
│   └── MathFunctions/
│       ├── MyAdd/
│       │   ├── my_add.cpp
│       │   └── my_add.h
│       ├── MySqrt/
│       │   ├── my_sqrt.cpp
│       │   └── my_sqrt.h
│       ├── CMakeLists.txt
│       ├── math_functions.cpp
│       └── math_functions.h
├── src/
│   └── main.cpp
├── CMakeLists.txt
└── config.h.in
```

**MathFunctions/CMakeLists.txt**

```cmake
option(USE_MYMATH "Use my math" ON)

#  MathFunctions
add_library(MathFunctions SHARED
    math_functions.h
    math_functions.cpp
)
target_include_directories(MathFunctions
    INTERFACE
    $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}>
    $<INSTALL_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>
)
target_compile_definitions(MathFunctions PRIVATE "USE_MYMATH")
target_compile_definitions(MathFunctions PRIVATE "EXPORTING_MYMATH")

set_property(TARGET MathFunctions PROPERTY VERSION "1.2.3")
set_property(TARGET MathFunctions PROPERTY SOVERSION "1")

if(USE_MYMATH)
    # MySqrt
    add_library(MySqrt SHARED
        MySqrt/my_sqrt.h
        MySqrt/my_sqrt.cpp
    )
    target_compile_definitions(MySqrt PRIVATE "EXPORTING_MYSQRT")
    target_include_directories(MySqrt
        INTERFACE
        $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/MySqrt>
    )

    # MyAdd
    add_library(MyAdd SHARED
        MyAdd/my_add.h
        MyAdd/my_add.cpp
    )
    target_compile_definitions(MyAdd PRIVATE "EXPORTING_MYADD")
    target_include_directories(MyAdd
        INTERFACE
        $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/MyAdd>
    )

    target_link_libraries(MathFunctions PRIVATE MySqrt)
    target_link_libraries(MathFunctions PRIVATE MyAdd)
endif()

set(installable_libs MathFunctions)
if(TARGET MySqrt)
    list(APPEND installable_libs MySqrt)
endif()
if(TARGET MyAdd)
    list(APPEND installable_libs MyAdd)
endif()

install(TARGETS ${installable_libs}
    RUNTIME DESTINATION bin
)
install(TARGETS MathFunctions
    LIBRARY DESTINATION lib
)
install(FILES math_functions.h
    DESTINATION include
)
```

**CMakeLists.txt**

```cmake
cmake_minimum_required(VERSION 3.10)

project(Step9 VERSION 1.9.1)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED True)

set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY "${PROJECT_BINARY_DIR}")
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY "${PROJECT_BINARY_DIR}")
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY "${PROJECT_BINARY_DIR}")

set(CMAKE_DEBUG_POSTFIX _debug)
set(CMAKE_RELEASE_POSTFIX _release)

configure_file(config.h.in config.h)

add_subdirectory(3rdParty/MathFunctions)

add_executable(Step9 src/main.cpp)
target_include_directories(Step9 PRIVATE ${CMAKE_BINARY_DIR})
target_link_libraries(Step9 PUBLIC MathFunctions)

# set_target_properties(Step9 PROPERTIES
#     DEBUG_POSTFIX ${CMAKE_DEBUG_POSTFIX}
#     RELEASE_POSTFIX ${CMAKE_RELEASE_POSTFIX}
# )

install(TARGETS ${CMAKE_PROJECT_NAME}
    RUNTIME DESTINATION bin
)

include(CTest)
add_test(NAME Runs COMMAND Step9 25)
set_tests_properties(Runs
    PROPERTIES PASS_REGULAR_EXPRESSION "The square root of [0-9 is [0-9]+"
)

function(do_sqr_test target arg result)
    add_test(NAME Sqr${arg}
        COMMAND ${target} ${arg}
    )
    set_tests_properties(Sqr${arg}
        PROPERTIES PASS_REGULAR_EXPRESSION ${result}
    )
endfunction()

do_sqr_test(Step9 4 "The square root of 4 is 2")
do_sqr_test(Step9 9 "The square root of 9 is 3")

function(do_add_test target x y ret)
    add_test(NAME Add${x}-${y}
        COMMAND ${target} ${x} ${y}
    )
    set_tests_properties(Add${x}-${y}
        PROPERTIES PASS_REGULAR_EXPRESSION ${ret}
    )
endfunction()

do_add_test(Step9 1 2 "The add result of [0-9. and [0-9. is [0-9.]+")
do_add_test(Step9 2 4 "The add result of [0-9. and [0-9. is [0-9.]+")

# set some CPACK variables
set(CPACK_PACKAGE_VERSION_MAJOR "${${PROJECT_NAME}_VERSION_MAJOR}")
set(CPACK_PACKAGE_VERSION_MINOR "${${PROJECT_NAME}_VERSION_MINOR}")
set(CPACK_PACKAGE_VERSION_MINOR "${${PROJECT_NAME}_VERSION_PATCH}")
set(CPACK_SOURCE_GENERATOR "7Z")

# include CPACK module
include(CPACK)
```

**build.ps1**

```powershell
if((Test-Path build) -eq $true) {
    Remove-Item -Path build/** -Recurse
}
else {
    New-Item -Path . -Name .\build -ItemType Directory
}

Push-Location build

$config_type = 'Debug'

mkdir $config_type

cmake -S .. -B $config_type -DUSE_MYMATH=ON
cmake --build ./$config_type --config $config_type

cmake --install ./$config_type --config $config_type --prefix "./$config_type/install"

ctest -VV -C $config_type --test-dir ./$config_type

cpack -G ZIP -B ./$config_type -C $config_type --config ./$config_type/CPackConfig.cmake

$config_type = 'Release'

mkdir $config_type

cmake -S .. -B $config_type -DUSE_MYMATH=ON
cmake --build ./$config_type --config $config_type

cmake --install ./$config_type --config $config_type --prefix "./$config_type/install"

ctest -VV -C $config_type --test-dir ./$config_type

cpack -G ZIP -B ./$config_type -C $config_type --config ./$config_type/CPackConfig.cmake

Pop-Location
```

## References

1. [CMake Tutorial — CMake 3.24.4 Documentation](https://cmake.org/cmake/help/v3.24/guide/tutorial/index.html#guide:CMake%20Tutorial)
[CMake Tutorial — CMake 3.24.4 Documentation.html](https://www.yuque.com/attachments/yuque/0/2023/html/22048361/1704035063217-33ee4188-8b75-48f2-8bbc-7828e6064ebe.html)
2. [Step 1_ A Basic Starting Point — CMake 3.24.4 Documentation.html](https://www.yuque.com/attachments/yuque/0/2023/html/22048361/1704035123693-4686e9db-28dd-4322-9c45-cb5a0c8b6f32.html)
3. [Step 2_ Adding a Library — CMake 3.24.4 Documentation.html](https://www.yuque.com/attachments/yuque/0/2023/html/22048361/1704035173056-f6fb8145-0e34-4e2d-9307-ea8293c9d850.html)
4. [Step 3_ Adding Usage Requirements for a Library — CMake 3.24.4 Documentation.html](https://www.yuque.com/attachments/yuque/0/2023/html/22048361/1704035202685-134c12db-5eab-440b-b3ed-4b638bae162e.html)
5. [Step 4_ Installing and Testing — CMake 3.24.4 Documentation.html](https://www.yuque.com/attachments/yuque/0/2023/html/22048361/1704035238656-823f86de-9b8c-4887-bdb9-f617ed681b0e.html)
6. [Step 5_ Adding System Introspection — CMake 3.24.4 Documentation.html](https://www.yuque.com/attachments/yuque/0/2023/html/22048361/1704035277102-dbf1b326-148f-4510-9f81-488e53a51b3e.html)
7. [Step 6_ Adding a Custom Command and Generated File — CMake 3.24.4 Documentation.html](https://www.yuque.com/attachments/yuque/0/2023/html/22048361/1704035305185-3691fbda-1f9f-446d-9e27-ced929ede5b3.html)
8. [Step 7_ Packaging an Installer — CMake 3.24.4 Documentation.html](https://www.yuque.com/attachments/yuque/0/2023/html/22048361/1704035331053-cd6f76a4-dcf7-4173-9951-7b3a7d743fa3.html)
9. [Step 8_ Adding Support for a Testing Dashboard — CMake 3.24.4 Documentation.html](https://www.yuque.com/attachments/yuque/0/2023/html/22048361/1704035356827-2750c6ee-8f48-43cb-b3f1-7bb3b26cf42a.html)
10. [Step 9_ Selecting Static or Shared Libraries — CMake 3.24.4 Documentation.html](https://www.yuque.com/attachments/yuque/0/2023/html/22048361/1704035385877-15509b88-e8a4-48a7-9ac3-cecf01333d19.html)
11. [Step 10_ Adding Generator Expressions — CMake 3.24.4 Documentation.html](https://www.yuque.com/attachments/yuque/0/2023/html/22048361/1704035417237-e9c35c23-91f0-42c8-99e0-85e80d998c08.html)
12. [Step 11_ Adding Export Configuration — CMake 3.24.4 Documentation.html](https://www.yuque.com/attachments/yuque/0/2023/html/22048361/1704035442493-d753b688-3d78-4b6b-b1ab-63e079a8b46c.html)
13. [Step 12_ Packaging Debug and Release — CMake 3.24.4 Documentation.html](https://www.yuque.com/attachments/yuque/0/2023/html/22048361/1704035469865-b0ecd89d-16ef-4dda-bf1b-c1e7a239f12e.html)
