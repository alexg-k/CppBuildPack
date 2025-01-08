cmake_minimum_required(VERSION 3.24)

### SETUP
project(CppBuildPack
    VERSION 1.0
    HOMEPAGE_URL "https://github.com/xyz"
    DESCRIPTION "My template for applications built with cmake"
    LANGUAGES CXX)


set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

## TARGETS
add_executable(${CMAKE_PROJECT_NAME})
add_subdirectory(src/)

### TEST
if(CMAKE_BUILD_TYPE STREQUAL "Debug")
    enable_testing()
    add_subdirectory(test/)
endif()

### INSTALL
include(GNUInstallDirs)
include(InstallRequiredSystemLibraries)

install(
    TARGETS ${PROJECT_NAME}
    LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR}
    RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR}
    ARCHIVE DESTINATION ${CMAKE_INSTALL_LIBDIR}
    BUNDLE  DESTINATION .
)

if(LINUX)
    configure_file(
        ${CMAKE_SOURCE_DIR}/pack/linux/${CMAKE_PROJECT_NAME}.desktop.in
        ${CMAKE_BINARY_DIR}/${CMAKE_PROJECT_NAME}.desktop
        @ONLY
    )
        install(
        FILES ${CMAKE_BINARY_DIR}/${CMAKE_PROJECT_NAME}.desktop
        DESTINATION ${CMAKE_INSTALL_DATADIR}/applications/
    )
    configure_file(
        ${CMAKE_SOURCE_DIR}/pack/linux/appimage/AppRun.in
        ${CMAKE_BINARY_DIR}/AppRun
        @ONLY
    )
    install(
        FILES ${CMAKE_SOURCE_DIR}/res/icons/appicon.png
        DESTINATION ${CMAKE_INSTALL_DATADIR}/icons/hicolor/128x128/apps/
        RENAME icon.png
    )
    set(CMAKE_INSTALL_PREFIX "/usr")
    install(SCRIPT "${CMAKE_SOURCE_DIR}/cmake/CreateAppImage.cmake")
endif()