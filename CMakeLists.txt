cmake_minimum_required(VERSION 3.2)

project(Example)

include(CTest)

include(DownloadProject.cmake)
download_project(PROJ                googletest
                 GIT_REPOSITORY      https://github.com/google/googletest.git
                 GIT_TAG             master
                 UPDATE_DISCONNECTED 1
)

# Override googletest defaults for these
option(BUILD_GTEST "Build gtest" ON)
option(BUILD_GMOCK "Build gmock" ON)

add_subdirectory(${googletest_SOURCE_DIR} ${googletest_BINARY_DIR} EXCLUDE_FROM_ALL)

# At time of writing, gtest and gmock don't add a public include directory
# to their respective targets for their headers, so we have to explicitly
# add them ourselves so that client code finds gtest/gtest.h and gmock/gmock.h
target_include_directories(gtest      INTERFACE "${gtest_SOURCE_DIR}/include")
target_include_directories(gmock_main INTERFACE "${gmock_SOURCE_DIR}/include")

# Trivial example using gtest and gmock
add_executable(example example.cpp)
target_link_libraries(example gtest gmock_main)
add_test(NAME example_test COMMAND example)