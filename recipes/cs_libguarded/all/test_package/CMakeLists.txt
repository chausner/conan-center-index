cmake_minimum_required(VERSION 3.15)
project(test_package LANGUAGES CXX)

add_executable(${PROJECT_NAME} test_package.cpp)

find_package(cs_libguarded CONFIG)
if (cs_libguarded_FOUND)
    target_link_libraries(${PROJECT_NAME} PRIVATE cs_libguarded::cs_libguarded)
    target_compile_features(${PROJECT_NAME} PRIVATE cxx_std_14)
else()
    find_package(CsLibGuarded REQUIRED CONFIG)
    target_link_libraries(${PROJECT_NAME} PRIVATE CsLibGuarded::CsLibGuarded)
    target_compile_definitions(${PROJECT_NAME} PRIVATE CS_LIBGUARDED_1_3_0_LATER)
    target_compile_features(${PROJECT_NAME} PRIVATE cxx_std_17)
endif()
