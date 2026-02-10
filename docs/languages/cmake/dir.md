# Dir

## PROJECT_BINARY_DIR

project build directory

## PROJECT_SOURCE_DIR

project source directory

## CMAKE_CURRENT_SOURCE_DIR

current directory of CMakeLists.txt

## CMAKE_CURRENT_BINARY_DIR

current project build directory

## CMAKE_CURRENT_LIST_DIR

full directory of the listfile currently being processed

## CMAKE_ARCHIVE_OUTPUT_DIRECTORY

set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY "${PROJECT_BINARY_DIR}")

## CMAKE_LIBRARY_OUTPUT_DIRECTORY

set(CMAKE_LIBRARY_OUTPUT_DIRECTORY "${PROJECT_BINARY_DIR}")

## CMAKE_RUNTIME_OUTPUT_DIRECTORY

set(CMAKE_RUNTIME_OUTPUT_DIRECTORY "${PROJECT_BINARY_DIR}")

## CMAKE_PREFIX_PATH

searched by the following commands:
* `find_package`
* `find_library`
* `find_program`
* `find_file`

## packagename_DIR

search for the specified package
