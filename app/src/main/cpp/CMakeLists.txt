cmake_minimum_required(VERSION 3.4.1)

#1. Set the location of the header file of the third-party library, which is the same level as CMakeLists.txt, so directly write include
include_directories(include)

#2. Import third-party dynamic library
add_library(avcodec SHARED IMPORTED)

set_target_properties( avcodec
        PROPERTIES
        IMPORTED_LOCATION ${CMAKE_SOURCE_DIR}/../jniLibs/${ANDROID_ABI}/libavcodec.so)
add_library(avformat SHARED IMPORTED)

set_target_properties( avformat
        PROPERTIES
        IMPORTED_LOCATION ${CMAKE_SOURCE_DIR}/../jniLibs/${ANDROID_ABI}/libavformat.so)

add_library(avutil SHARED IMPORTED)
set_target_properties( avutil
        PROPERTIES
        IMPORTED_LOCATION ${CMAKE_SOURCE_DIR}/../jniLibs/${ANDROID_ABI}/libavutil.so)

add_library(swscale SHARED IMPORTED)
set_target_properties( swscale
        PROPERTIES
        IMPORTED_LOCATION ${CMAKE_SOURCE_DIR}/../jniLibs/${ANDROID_ABI}/libswscale.so)

#3. Create a dynamic library (the dynamic library that you will generate, the library name and code file can be changed as needed, just show it here)
add_library( TestJNI SHARED native-lib.cpp)


find_library( # Sets the name of the path variable.
        log-lib

        # Specifies the name of the NDK library that
        # you want CMake to locate.
        log)


# 4. Third-party dynamic libraries required for linking
target_link_libraries( # Specifies the target library.
TestJNI

#the third library
avcodec
avformat
avutil
swscale

# Links the target library to the log library
# included in the NDK.
${log-lib})