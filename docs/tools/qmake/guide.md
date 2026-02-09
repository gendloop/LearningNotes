# Guide

The qmake tool helps simplify the build process for development projects across different platforms.

Function as follows:

* generates a Makefile based on the information in a project file
* contains additional features to support development with Qt, automatically including build rules for moc and uic
* generate projects for Microsoft Visual Studio without changing the project file

## Overview

### Describing a Project

Projects are described by the contents of project files (.pro)

Project files contain:

* comments
* variable declareations
* built-in functions
* control structures
* source files
* header files
* configuration options

## Tutorial

This tutorials teaches you the basics of qmake

### Starting Off Simple

1. Create a directory tree like this

```plain
2.1
├── 2.1.pro
└── src
    ├── hello.cpp
    ├── hello.h
    └── main.cpp
```

1. use `SOURCES` variable to add the sources files to the project file (2.1.pro)

```plain
SOURCES +=
```

## References

1. [qmake.7z](https://www.yuque.com/attachments/yuque/0/2024/7z/22048361/1735097718361-151db105-b733-4998-a3d5-b97a39198986.7z)
2. [qmake-manual.html](https://www.yuque.com/attachments/yuque/0/2024/html/22048361/1709561606747-96826586-61da-4742-8a08-adf034ea1c5c.html)
3. [qmake-overview.html](https://www.yuque.com/attachments/yuque/0/2024/html/22048361/1709562793107-ff14448c-7190-4379-a37b-3539e237f239.html)
4. [qmake-tutorial.html](https://www.yuque.com/attachments/yuque/0/2024/html/22048361/1709562865602-97bf51e6-e55f-40ce-8141-d7a81cca09d3.html)
