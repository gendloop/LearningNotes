# Func

## "cmake_minimum_required"

cmake_minimum_required(VERSION 3.10)

## "project"

project(Tutorials)
project(Tutorials VERSION 2.0)
project(${PROJECT_NAME}                                                                                          |            |              |

##

VERSION ${${PROJECT_NAME}_VERSION_MAJOR}                                                                         |            |              |

##

               .${${PROJECT_NAME}_VERSION_MINOR}                                                                 |            |              |

##

               .${${PROJECT_NAME}_VERSION_PATCH})                                                                |            |              |

## "add_executable"

add_executable(Tutorial src/tutorials.cxx)                                                                       | √          | √            |

## "configure_file"

config_file(config.h.in config.h)                                                                                | √          | √            |

## "target_include_directories"

target_include_directories(Tutorial                                                                              | √          | √            |

##

    PUBLIC "${PROJECT_BINARY_DIR}"                                                                               |            |              |

##

)                                                                                                                |            |              |

##

                                                                                                                 |            |              |

##

target_include_directories(MathFunctions                                                                         |            |              |

##

    INTERFACE ${CMAKE_CURRENT_SOURCE_DIR}                                                                        |            |              |

##

)                                                                                                                |            |              |

##

                                                                                                                 |            |              |

##

target_include_director ies(${PROJECT_NAME}                                                                      |            |              |

##

    INTERFACE include                                                                                            |            |              |

##

)                                                                                                                |            |              |

##

                                                                                                                 |            |              |

##

target_include_directories(MathFunctions                                                                         |            |              |

##

    INTERFACE                                                                                                    |            |              |

##

    $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}>                                                               |            |              |

##

    $<INSTALL_INTERFACE:include>                                                                                 |            |              |

##

)                                                                                                                |            |              |

## "add_library"

add_library(MathFunctions mysqrt.cxx)                                                                            | √          | √            |

##

                                                                                                                 |            |              |

##

add_library(${PROJECT_NAME} SHARED                                                                               |            |              |

##

    ${SRC_FILES}                                                                                                 |            |              |

##

)                                                                                                                |            |              |

##

                                                                                                                 |            |              |

##

add_library(${PROJECT_NAME}_static STATIC                                                                        |            |              |

##

    ${SRC_FILES}                                                                                                 |            |              |

##

)                                                                                                                |            |              |

## "add_subdirectory"

add_subdirectory(3rdParty/MathFunctions)                                                                         | √          | √            |

## "target_link_libraries"

target_link_libraries(Step2 PUBLIC                                                                               | √          | √            |

##

    MathFunctions                                                                                                |            |              |

##

)                                                                                                                |            |              |

## "option"

option(USE_MATH "Use my math functions" ON)                                                                      | √          | √            |

## "if"

if(USE_MATH)                                                                                                     | √          | nan          |

##

    add_subdirectory(3rdParty/MathFunctions)                                                                     |            |              |

##

    list(APPEND EXTRA_LIBS MathFunctions)                                                                        |            |              |

##

    list(APPEND EXTRA_INCLUDES                                                                                   |            |              |

##

        "${PROJECT_SOURCE_DIR}/3rdParty/MathFunctions")                                                          |            |              |

##

endif()                                                                                                          |            |              |

##

                                                                                                                 |            |              |

##

if(HAVE_LOG AND HAVE_EXP)                                                                                        |            |              |

##

    target_compile_definitions(MathFunctions                                                                     |            |              |

##

        PRIVATE "HAVE_LOG" "HAVE_EXP"                                                                            |            |              |

##

    )                                                                                                            |            |              |

##

endif()                                                                                                          |            |              |

##

                                                                                                                 |            |              |

##

if(line MATCHES "=")                                                                                             |            |              |

##

    string(REGEX MATCH "^[^=]*" name ${line})                                                                    |            |              |

##

    string(REGEX MATCH "[^=]*$" value ${line})                                                                   |            |              |

##

    set(${name} ${value})                                                                                        |            |              |

##

endif()                                                                                                          |            |              |

##

                                                                                                                 |            |              |

##

if(TARGET MySqrt)                                                                                                |            |              |

##

    list(APPEND installable_libs MySqrt)                                                                         |            |              |

##

endif()                                                                                                          |            |              |

## "list"

list(APPEND EXTRA_LIBS MathFunctions)                                                                            | √          | √            |

## "install"

install(TARGETS MathFunctions                                                                                    | √          | √            |

##

    DESTINATION lib                                                                                              |            |              |

##

)                                                                                                                |            |              |

##

                                                                                                                 |            |              |

##

install(FILES MathFunctions.h                                                                                    |            |              |

##

    DESTINATION include/MathFunctions                                                                            |            |              |

##

)                                                                                                                |            |              |

##

                                                                                                                 |            |              |

##

install(TARGETS ${PROJECT_NAME} ${PROJECT_NAME}_static                                                           |            |              |

##

    LIBRARY DESTINATION lib                                                                                      |            |              |

##

    ARCHIVE DESTINATION lib                                                                                      |            |              |

##

    RUNTIME DESTINATION bin                                                                                      |            |              |

##

    INCLUDES DESTINATION include                                                                                 |            |              |

##

)                                                                                                                |            |              |

##

                                                                                                                 |            |              |

##

install(DIRECTORY include/                                                                                       |            |              |

##

    DESTINATION include                                                                                          |            |              |

##

)                                                                                                                |            |              |

##

                                                                                                                 |            |              |

##

                                                                                                                 |            |              |

##

install(TARGETS ${installable_libs}                                                                              |            |              |

##

    EXPORT MathFunctionsTargets                                                                                  |            |              |

##

    LIBRARY DESTINATION lib                                                                                      |            |              |

##

)                                                                                                                |            |              |

##

install(EXPORT MathFunctionsTargets                                                                              |            |              |

##

    FILE MathFunctionsTargets.cmake                                                                              |            |              |

##

    NAMESPACE ${PROJECT_NAME}::                                                                                  |            |              |

##

    DESTINATION lib/cmake/MathFunctions                                                                          |            |              |

##

)                                                                                                                |            |              |

## "add_test"

enable_testing()                                                                                                 | √          | √            |

##

add_test(NAME Usage COMMAND Step2)                                                                               |            |              |

## "set_tests_properties"

set_tests_properties(Usage                                                                                       | √          | nan          |

##

    PROPERTIES_PASS_REGULAR_EXPRESSION "VERSION_MAJOR: .*"                                                       |            |              |

##

)                                                                                                                |            |              |

## "function"

function(do_test target arg result)                                                                              | √          | √            |

##

    add_test(NAME Comp${arg} COMMAND ${target} ${arg})                                                           |            |              |

##

    set_tests_properties(Comp${arg}                                                                              |            |              |

##

        PROPERTIES PASS_REGULAR_EXPRESSION ${result}                                                             |            |              |

##

    )                                                                                                            |            |              |

##

endfunction()                                                                                                    |            |              |

## "check_cxx_source_compiles"

include(CheckCXXSourceCompiles)                                                                                  | √          | √            |

##

check_cxx_source_compiles("                                                                                      |            |              |

##

    #include <cmath>                                                                                             |            |              |

##

    int main() {                                                                                                 |            |              |

##

        std::log(1.0);                                                                                           |            |              |

##

        return 0;                                                                                                |            |              |

##

    }                                                                                                            |            |              |

##

" HAVE_LOG)                                                                                                      |            |              |

## "target_compile_definitions"

target_compile_definitions(MathFunctions                                                                         | √          | √            |

##

    PRIVATE "HAVE_LOG" "HAVE_EXP"                                                                                |            |              |

##

)                                                                                                                |            |              |

##

                                                                                                                 |            |              |

##

target_compile_definitions(                                                                                      |            |              |

##

    PRIVATE "XI_DLL" "_CRT_SECURE_NO_WARNNIGS"                                                                   |            |              |

##

)                                                                                                                |            |              |

## "add_custom_command"

add_custom_command(                                                                                              | √          | √            |

##

    OUPUT ${PROJECT_SOURCE_DIR}/src/a_table.h                                                                    |            |              |

##

    COMMAND MakeATable ${PROJECT_SOURCE_DIR}/src/a_table.h                                                       |            |              |

##

    DEPENDS MakeATable                                                                                           |            |              |

##

)                                                                                                                |            |              |

## "enable_testing"

enable_testing()                                                                                                 | √          | √            |

## "include"

include(CheckCXXSourceCompiles)                                                                                  | √          | √            |

##

                                                                                                                 |            |              |

##

include(InstallRequiredSystemLibraries)                                                                          |            |              |

##

                                                                                                                 |            |              |

##

include(CPACK)                                                                                                   |            |              |

##

                                                                                                                 |            |              |

##

include(CTest)                                                                                                   |            |              |

##

                                                                                                                 |            |              |

##

include(CMakePackageConfigHelpers)                                                                               |            |              |

## "file"

file(STRINGS "config.txt" CONFIG_CONTENT)                                                                        | √          | nan          |

##

                                                                                                                 |            |              |

##

file(GLOB_RECURSE SRC_FILES "src/*.cpp" "src/*.h")                                                               |            |              |

##

                                                                                                                 |            |              |

##

file(GLOB SRC_FILES "src/*.cpp" "src/*.h")                                                                       |            |              |

## "foreach"

foreach(line ${CONFIG_CONTENT})                                                                                  | √          | nan          |

##

    string(REGEX MTACH "^[^#]*" line ${line})                                                                    |            |              |

##

    if(line MATCHED "=")                                                                                         |            |              |

##

        string(REGEX MATCH "^[^=]*" name ${line})                                                                |            |              |

##

        string(REGEX MATCH "[^=]*$" value ${line})                                                               |            |              |

##

        set(${name} ${value})                                                                                    |            |              |

##

    endif()                                                                                                      |            |              |

##

endforeach()                                                                                                     |            |              |

## "set"

set(CMAKE_CXX_STANDARD 11)                                                                                       | √          | √            |

##

                                                                                                                 |            |              |

##

set(CMake_CXX_STANDARD_REQUIRED True)                                                                            |            |              |

##

                                                                                                                 |            |              |

##

set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY "${PROJECT_BINARY_DIR}")                                                      |            |              |

##

                                                                                                                 |            |              |

##

set(CMAKE_LIBRARY_OUTPUT_DIRECTORY "${PROJECT_BINARY_DIR}")                                                      |            |              |

##

                                                                                                                 |            |              |

##

set(CMAKE_RUNTIME_OUTPUT_DIRECTORY "${PROJECT_BINARY_DIR}")                                                      |            |              |

## "configure_package_config_file"

include(CMakePackageConfigHelpers)                                                                               | √          | √            |

##

configure_package_config_file(                                                                                   |            |              |

##

    ${PROJECT_SOURCE_DIR}/config.cmake.in                                                                        |            |              |

##

    ${PROJECT_BINARY_DIR}/MathFunctionsConfig.cmake                                                              |            |              |

##

    INSTALL_DESTINATION lib/cmake/MathFunctions                                                                  |            |              |

##

    NO_SET_AND_CHECK_MACRO                                                                                       |            |              |

##

    NO_CHECK_REQUIRED_COMPONENTS_MACRO                                                                           |            |              |

##

)                                                                                                                |            |              |

## "write_basic_package_version_file"

write_basic_package_version_file(                                                                                | √          | √            |

##

    "${CMAKE_CURRENT_BINARY_DIR}/MathFunctionsConfigVersion.cmake"                                               |            |              |

##

    VERSION "${${PROJECT_NAME}_VERSION_MAJOR}.${${PROJECT_NAME}_VERSION_MINOR}.${${PROJECT_NAME}_VERSION_PATCH}" |            |              |

##

    COMPATIBILITY AnyNewerVersion                                                                                |            |              |

##

)                                                                                                                |            |              |

## "export"

export(EXPORT MathFunctionsTargets                                                                               | √          | √            |

##

    FILE "${CMAKE_CURRENT_BINARY_DIR}/MathFunctionsTargets.cmake"                                                |            |              |

##

)                                                                                                                |            |              |

## "find_package"

find_package(MathFunctions CONFIG REQUIRED)                                                                      | √          | √            |

##

                                                                                                                 |            |              |

##

find_package(MathFunctions CONFIG                                                                                |            |              |

##

    REQUIRED COMPONENTS Step9::MyAdd                                                                             |            |              |

##

)                                                                                                                |            |              |

## "source_group"

source_group("" FILES ${SRC_FILES})                                                                              | √          | √            |

##

                                                                                                                 |            |              |

##

source_group("Add" FILES ${SRC_ADD_FILES})                                                                       |            |              |

## "set_property"

set_property(DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}                                                               | √          | √            |

##

    PROPERTY VS_STARTUP_PROJECT ${PROJECT_NAME})                                                                 |            |              |
