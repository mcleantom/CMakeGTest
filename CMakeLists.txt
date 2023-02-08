cmake_minimum_required(VERSION 3.26)
project(unittest_test)


include(FetchContent)

FetchContent_Declare(
  googletest
  GIT_REPOSITORY https://github.com/google/googletest.git
  GIT_TAG        703bd9caab50b139428cea1aaff9974ebee5742e # release-1.10.0
  SYSTEM
)

FetchContent_MakeAvailable(googletest)

set(CMAKE_CXX_STANDARD 17)

enable_testing()

file(GLOB_RECURSE unittests_src CONFIGURE_DEPENDS "*.cpp")

set(CMAKE_COMPILE_WARNING_AS_ERROR OFF)
set_target_properties(gtest gtest_main PROPERTIES COMPILE_WARING_AS_ERROR OFF)

target_compile_options(gtest PRIVATE "-w")

add_executable(
    unittests
    "rununittests.cpp"
    "test_one.cpp"
)

target_link_libraries(
    unittests
    PUBLIC
    gtest
    gtest_main
)

add_test(
    NAME
    unittests
    COMMAND
    ${CMAKE_BINARY_DIR}/${CMAKE_INSTALL_BINDIR}/unit_tests
)