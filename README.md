# conan-cpp-demo
Example timer with POCO C++ libraries installed with conan C and C++ package manager

#### Add App Dependencies : poco

```
conan-cpp-demo$ conan remote list
conancenter: https://center.conan.io [Verify SSL: True]

conan-cpp-demo$ conan search poco* --remote=conancenter
Existing package recipes:

poco/1.8.1
poco/1.9.3
poco/1.9.4
poco/1.10.0
poco/1.10.1
poco/1.11.0
poco/1.11.1
poco/1.11.2

```
#### Create conanfile.txt 
```
conan-cpp-demo$ vim conanfile.txt 

[requires]
poco/1.8.1

[generators]
cmake

```
#### Create a build directory with `mkdir build`, and `cd build`.
```
conan-cpp-demo $ mkdir build && cd build
```
#### Run `conan install`, passing the directory where your `conanfile.txt` is,
#### to download and install dependencies and generate the `conanbuildinfo.cmake` used by `CMakeLists.txt`.
#### For example, run `conan install ..` if your `conanfile.txt` is in the parent directory.

```
conan-cpp-demo/build$ conan install ..

conan-cpp-demo/build$ ls | grep build
conanbuildinfo.cmake

```
#### Create `CMakeLists.txt` in project directory
```
conan-cpp-demo/build$ vim ../CMakeLists.txt

project(FoundationTimer)
cmake_minimum_required(VERSION 2.8.12)

include(${CMAKE_BINARY_DIR}/conanbuildinfo.cmake)
conan_basic_setup()

add_executable(timer timer.cpp)
target_link_libraries(timer ${CONAN_LIBS})
```
#### Run the build system, `cmake`, in the directory containing your `CMakeLists.txt` to create the `Makefile`.
#### Run`make` to build your program using the generated `Makefile`.
```
conan-cpp-demo/build$ cmake ..
conan-cpp-demo/build$ make 
  ... Linking CXX executable bin/timer
```
#### Run binary `timer`
```
conan-cpp-demo/build$ ./bin/timer 
Callback called after 250 milliseconds.
Callback called after 750 milliseconds.
Callback called after 1250 milliseconds.
Callback called after 1751 milliseconds.

```
