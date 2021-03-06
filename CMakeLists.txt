cmake_minimum_required(VERSION 3.0.2 FATAL_ERROR)

project(lxqt-powermanagement)

include(GNUInstallDirs)

set(CMAKE_AUTOMOC ON)
set(CMAKE_AUTOUIC ON)
set(CMAKE_INCLUDE_CURRENT_DIR ON)
set(CMAKE_POSITION_INDEPENDENT_CODE ON)

option(UPDATE_TRANSLATIONS "Update source translation translations/*.ts files" OFF)

find_package(Qt5DBus REQUIRED)
find_package(Qt5LinguistTools REQUIRED QUIET)
find_package(Qt5Svg REQUIRED)
find_package(Qt5Widgets REQUIRED)
find_package(Qt5X11Extras REQUIRED)
message(STATUS "Building with Qt${Qt5Core_VERSION}")

find_package(KF5Solid REQUIRED)

find_package(lxqt REQUIRED)

if(NOT CMAKE_BUILD_TYPE)
    set(CMAKE_BUILD_TYPE Release)
endif()

set(LXQT_POWERMANAGEMENT_PATCH_VERSION 2)
set(LXQT_POWERMANAGEMENT_VERSION ${LXQT_MAJOR_VERSION}.${LXQT_MINOR_VERSION}.${LXQT_POWERMANAGEMENT_PATCH_VERSION})
add_definitions("-DLXQT_POWERMANAGEMENT_VERSION=\"${LXQT_POWERMANAGEMENT_VERSION}\"")

include(LXQtCompilerSettings NO_POLICY_SCOPE)

# Translations **********************************
include(LXQtTranslate)

add_subdirectory(config)
add_subdirectory(src)

# merged from lxqt-common
add_subdirectory(autostart)
