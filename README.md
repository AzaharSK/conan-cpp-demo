# conan-cpp-demo
Example timer with POCO C++ libraries installed with conan C and C++ package manager

### App Dependencies : poco

```
$ conan remote list
conancenter: https://center.conan.io [Verify SSL: True]

$ conan search poco* --remote=conancenter
Existing package recipes:

poco/1.8.1
poco/1.9.3
poco/1.9.4
poco/1.10.0
poco/1.10.1
poco/1.11.0
poco/1.11.1
poco/1.11.2

$ vim conanfile.txt 

[requires]
poco/1.8.1

[generators]
cmake

$ mkdir build && cd build
build$ conan install ..

build$ ls | grep build
conanbuildinfo.cmake

build$ vim ../CMakeLists.txt

project(FoundationTimer)
cmake_minimum_required(VERSION 2.8.12)

include(${CMAKE_BINARY_DIR}/conanbuildinfo.cmake)
conan_basic_setup()

add_executable(timer timer.cpp)
target_link_libraries(timer ${CONAN_LIBS})


build$ cmake ..
build$ make 

build$ ./bin/timer 
Callback called after 250 milliseconds.
Callback called after 750 milliseconds.
Callback called after 1250 milliseconds.
Callback called after 1751 milliseconds.

```
