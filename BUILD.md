# Building srcML

srcML is built using cmake, www.cmake.org, (version 2.8.12 or above) and currently supports builds for
macOS, Fedora, Ubuntu, CentOS, OpenSUSE, and Windows Visual Studio.

srcML使用cmake、www.cmake.org(版本2.8.12或更高)构建，目前支持macOS、Fedora、Ubuntu、CentOS、OpenSUSE和Windows Visual Studio的构建。

Out of source builds (builds outside the source directory) are required. In source builds are not supported.

需要脱离源代码构建(在源目录之外构建)。不支持源版本。

## Unix

To generate a makefile in your build directory:

    cmake <path_to_srcml>

 The following make commands are supported with their usual meaning

    make  
    make clean  
    make test  
    make install

 Client tests are enabled by default, while libsrcml and parser tests are disabled by default.
 These tests can be enabled/disabled via the cmake command, e.g. with a parallel source directory,

    cmake -DBUILD_CLIENT_TESTS=OFF -DBUILD_LIBSRCML_TESTS=ON -DBUILD_PARSER_TESTS=ON ../srcML

 You may need to run `ldconfig` to get the link to the libsrcml shared library path up to date

### macOS

The main packages required may be installed via brew:

    brew install antlr2 boost cmake

The srcML client requires at least LibArchive 3. macOS includes version 2.8. Because of this, LibArchive is
statically linked into the client. There are two options

* Use brew to install a more recent version:

    `brew install libarchive`

* Download and build LibArchive in a directory `libarchive` parallel to the source directory, typically \~/libarchive

To generate srcML documentation:

    brew install man2html doxygen

Additional packages that may not needed, but are recommended (for timing etc.):

    brew install coreutils gnu-sed gnu-time

#### Linux

Linux builds for Ubuntu, Fedora, CentOS and OpenSUSE are supported.

To find what is needed, it is recommended to consult these dockerfiles for the particular distribution:

* [Ubuntu](https://github.com/srcML/Docker/blob/ubuntu_latest/base/Dockerfile)
* [Fedora](https://github.com/srcML/Docker/blob/fedora_latest/base/Dockerfile)
* [CentOS](https://github.com/srcML/Docker/blob/centos_latest/base/Dockerfile)
* [OpenSUSE](https://github.com/srcML/Docker/blob/opensuse_latest/base/Dockerfile)

Commands to install what is needed can be adapted from these, and they are tested to work. You will also find dockerfiles for older versions of these distributions.

## Windows Using MSVC

Building in Windows requires that you have MSVC installed. Visual Studio 2017 or newer is known to work, while older versions have not been tested. This build only supports 64-bit binaries.

在Windows中构建需要安装MSVC。Visual Studio 2017或更新版本可以正常工作，而旧版本还没有经过测试。此版本只支持64位二进制文件。

## Packages

* [Java JRE/JDK](http://www.oracle.com/technetwork/java/javase/downloads/index.html)
* [CMake](http://www.cmake.org)
* [Visual Studio 2017 or later](https://www.visualstudio.com/downloads/)
* Zipped [Visual Studio 2017 Build Dependencies](http://www.sdml.cs.kent.edu/build/VS2017_Dependencies-06_20_18.zip)

##### Instructions
* Install Visual Studio 2017 or newer, CMake
* Locate the source code for srcML
* Extract the zipped build dependencies
    * The extracted folder will be named deps, and its structure will look like the following:

        ```
            deps/
                debug/
                include/
                release/
                tools/
        ```
    * When copied into the srcML source code directory the result should look like the following:

        ```
            srcML/  
                    BUILD.md
                    package/
                    CMakeLists.txt
                    COPYING.txt
                    CTestConfig.cmake
                    deps/
                        include/
                        tools/
                        x64/
                    doc/
                    ...etc...
        ```
* NOTES:
    * Building srcml should be done in a separate directory external to the source code to avoid issues
* Graphical Interface Build:
    * Open the CMake GUI program.
    * Browser for the srcML source code directory and your target build directory
    * Hit configure and select the appropriate Visual Studio version and x64 architecture as the target system.
    * Click Generate
    * Open srcML.sln with Visual Studio located in your the target build directory
    * Right click Project "ALL_BUILD" and choose "build"
* Command Line Buid:
    * Generate the build files in your target build directory.

        ```
            cmake [path to srcML source directory] -G [target visual studio version and architecture]   
        ```
        For example:

        ```
            cmake ..\srcML\ -G "Visual Studio 15 2017 Win64"
        ```
    * Execute the build.

        ```
            cmake --build . --config [build mode]
        ```
        For example:

        ```
            cmake --build . --config release
    ```

* Once built, locate the build folder. Within that folder there is now a directory named `bin` containing the release or debug versions of srcML executable and library along with all other dependencies.
