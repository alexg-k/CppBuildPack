# CppBuildPack

This is a minimal template procject to build C++ code in a modern build and package environment. For now, only Linux is supported, but more platforms might be added when a contributer requires them. For Linux the application is packaged as an AppImage. For adapting this repository to more complex projects, I recommend to make use of containers to build, test and package.

## Build and package
### Linux
To build and package, simply run in the project root directory:
1. `cmake -S . -B build`
2. `DESTDIR=AppDir/ cmake --build build --target install`

For more realistic projects the list fo dependencies will become more complex, so may want to create a docker image to build and package in. This simple example can be run with an existing docker image:
1. `docker run --rm -v ${PWD}:/project danger89/cmake:latest sh -c "cd /project && cmake -S . -B build_docker && DESTDIR=AppDir/ cmake --build build_docker --target install"`