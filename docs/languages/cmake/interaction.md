## About
+ This will detail 
    1. the steps needed to run the cmake or cmake-gui executable 
    2. how to choose a generator
    3. how to complete the build



## Setting Build Variables
### Commonly used CMake variables
| **Variable** | **Meaning** |
| --- | --- |
| `CMAKE_PREFIX_PATH` | Path to search for dependent packages |
| `CMAKE_MODULE_PATH` | Path to search for additional CMake modules |
| `CMAKE_BUILD_TYPE` | Configuration: `Debug`| `Release` |
| `CMAKE_INSTALL_PREFIX` | Path to install build target |
| `CMAKE_TOOLCHAIN_FILE` | File containing cross-compiling data    such as toolchains and sysroots. |
| `BUILD_SHARED_LIBS` | Build `shared libraries` | `static libraries` |
| `CMAKE_EXPORT_COMPLIE_COMMANDS` | Generate a `compile_commands.json` file    for use with clang-based tools |


## References
1. [User Interaction Guide — CMake 3.24.4 Documentation](https://cmake.org/cmake/help/v3.24/guide/user-interaction/index.html#guide:User%20Interaction%20Guide)   
[User Interaction Guide — CMake 3.24.4 Documentation.html](https://www.yuque.com/attachments/yuque/0/2023/html/22048361/1704034955581-e3826519-a90c-4d20-b186-95f119ab21d6.html) 

