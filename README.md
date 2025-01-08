# CppBuildPack

This is a minimal template project to build C++ code in a modern build and package environment. For now, only Linux is supported, but more platforms might be added when a contributer requires them. For Linux, the application is packaged as an [AppImage](https://appimage.org/).

## Build and package
### Linux
To build and package, simply run in the project root directory:
1. `cmake -S . -B build`
2. `cmake --build build --target all`
3. `DESTDIR=AppDir/ cmake --build build --target install`

For more realistic projects the list fo dependencies will become more complex, so may want to setup a ci/cd pipeline or create a docker image to build and package in. This simple example can be built with an existing docker image:
1. `docker run --rm -v ${PWD}:/project danger89/cmake:latest sh -c "cd /project && cmake -S . -B build_docker && cmake --build build_docker --target all && DESTDIR=AppDir/ cmake --build build_docker --target install"`

A ci/cd workflow for github is also added for the example.