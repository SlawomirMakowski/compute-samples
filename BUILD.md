# Build
CMake requires properly configured proxy settings using environmental variables: `HTTP_PROXY` and `HTTPS_PROXY`.
First build can take few minutes because all dependencies are set.

    git clone https://github.com/intel/compute-samples
    cd compute-samples
    mkdir build
    cd build
    cmake ..
    cmake --build .

In order to use a different generator than a default one please use `-G` option based on the [CMake documentation](https://cmake.org/cmake/help/v3.8/manual/cmake-generators.7.html). 
For example, you can generate a Visual Studio 2017 solution by running: `cmake .. -G "Visual Studio 15 2017"`

Note: If you have issues with building Boost with Visual Studio 2017 then please execute above commands using `Developer Command Prompt For VS 2017`.

Note: In order to build the project using GCC 8, Boost 1.68 is required, becasue of [this](https://github.com/boostorg/compute/issues/778) bug in Boost::Compute.

# Installation
The following command installs project's binaries.
By default they are installed in the `build` directory, but it can be customized by adding `CMAKE_INSTALL_PREFIX=your/path` during CMake configuration.

    cmake --build . --target install

# Package
In order to create a redistributable package please use the following command:

    cmake --build . --target package

# Source Package
In order to create a redistributable source package please use the following command:

    cmake --build . --target package_source

# CMake options
CMake can be configured using the following parameters:

* `BUILD_BOOST` - If set to `OFF` then Boost won't be downloaded and built during CMake configuration. Default is `ON`.
Please note that most of the time to build the project the first time is in downloading and building Boost.
* `BOOST_ROOT` - Path to the custom Boost installation directory.
* `BUILD_PNG` - If set to `OFF` then libpng won't be downloaded and built during CMake configuration. Default is `ON`.
* `PNG_ROOT` - Path to the custom libpng installation directory.
* `ZLIB_ROOT` - Path to the custom zlib installation directory.
* `DOWNLOAD_MEDIA` - If set to `OFF` media files to use as inputs for sample application won't be downloaded. Default in `ON`.
* `MEDIADATA_ROOT` - Path to the mediadata directory. It is only relevant if `DOWNLOAD_MEDIA` is set to `OFF`.
* `DOWNLOAD_GTEST` - If set to `OFF` then Google Test won't be downloaded during CMake configuration. Default is `ON`.
* `GTEST_ROOT` - Path to the custom Google Test installation directory.
* `BUILD_OPENCL` - If set to `OFF` then OpenCL ICD won't be downloaded and built during CMake configuration. Default is `ON`.
* `OPENCL_ROOT` - Path to the custom OpenCL ICD installation directory.

Example command line: `cmake .. -DBUILD_BOOST=OFF -DBOOST_ROOT=/home/boost_1_64_0`

# Dependencies
* [Boost 1.64](http://www.boost.org/)
* [libpng 1.6.30](http://www.libpng.org/pub/png/libpng.html)
* [Google Test 1.8.1](https://github.com/google/googletest)

# Test
There are 3 ways to run tests depending on the use case:

* To run all registered tests from all modules run `ctest` from the `build` directory.
* To run all tests from a specific module find module's tester and run it.
* To run specific tests from a specific module find module's tester and run it with `--gtest_filter` option or use the `ctest -R *test_pattern*` option.

If you want to run `ctest` on a different configuration like `Debug` or `Release` please use `-C` option according to the [CTest documentation](https://cmake.org/cmake/help/v3.8/manual/ctest.1.html).
