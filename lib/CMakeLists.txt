cmake_minimum_required(VERSION 3.9)
project(comparepackages VERSION 1.0.0 DESCRIPTION "lib to compare packages")

include(GNUInstallDirs)
find_package(CURL REQUIRED)
find_package(Boost 1.76 REQUIRED)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

add_library(comparepackages SHARED src/comparepackages.cpp)
add_library(boost INTERFACE)

set_target_properties(comparepackages PROPERTIES
        VERSION ${PROJECT_VERSION}
        SOVERSION ${PROJECT_VERSION_MAJOR}
        PUBLIC_HEADER include/comparepackages.hpp)

target_include_directories(comparepackages PRIVATE .)
target_include_directories(boost INTERFACE /usr/local/boost_1_76_0)

target_link_libraries(comparepackages PRIVATE boost curl)

install(TARGETS comparepackages
        LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR}
        PUBLIC_HEADER DESTINATION ${CMAKE_INSTALL_INCLUDEDIR})