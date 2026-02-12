# Dir

## PROJECT_BINARY_DIR

Project build directory

## PROJECT_SOURCE_DIR

Project source directory

## CMAKE_CURRENT_SOURCE_DIR

Current directory of CMakeLists.txt

## CMAKE_CURRENT_BINARY_DIR

Current project build directory

## CMAKE_CURRENT_LIST_DIR

Full directory of the listfile currently being processed

## CMAKE_ARCHIVE_OUTPUT_DIRECTORY

```cmake
set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY "${PROJECT_BINARY_DIR}")
```

## CMAKE_LIBRARY_OUTPUT_DIRECTORY

```cmake
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY "${PROJECT_BINARY_DIR}")
```

## CMAKE_RUNTIME_OUTPUT_DIRECTORY

```cmake
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY "${PROJECT_BINARY_DIR}")
```

## CMAKE_PREFIX_PATH

Searched by the following commands:
* `find_package`
* `find_library`
* `find_program`
* `find_file`

## packagename_DIR

Search for the specified package
