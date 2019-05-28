Taken information from: </br>
"http://derekmolloy.ie/hello-world-introductions-to-cmake/" <br>
"https://fedetft.wordpress.com/2009/12/21/cmake-part-2-compiler-flags/" <br>

To see exactly what CMake does to compile files use the commands:

```
mkdir build && cd build
cmake ../
make VERBOSE=1
```

To switch between Release and Debug mode, you can specify the option in the CMake command line:

```
mkdir build && cd build
cmake -D CMAKE_BUILD_TYPE=Debug ../
make
```

Or simply specify a build type in the CMakeLists.txt file:

```
set(CMAKE_BUILD_TYPE Release)
```

To speed up builds, you can use the ```-jX``` option of make, where X is the number of cores in your CPU. It tells make to compile X files at the same time. So for a dual core, use:

```
mkdir build && cd build
cmake ../
make -j2
```