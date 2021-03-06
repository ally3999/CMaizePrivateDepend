cmake_minimum_required(VERSION 3.13.4)
project(CMaize_Private_Depend)

include("${PROJECT_SOURCE_DIR}/cmake/get_cpp.cmake")

#must use a new token to access private library (this one unusable after pushing in git)
set(CPP_GITHUB_TOKEN f64bff2118e84de749f10dec47ddc97a078e7082)

cpp_find_or_build_dependency(
    CMakePrivate
    PRIVATE true
    URL github.com/CMaizeExamples/CMakePrivate
    VERSION ally #for testing purposes, use the branch "ally" -- can comment this out once changes are approved by master
    BUILD_TARGET CMakePrivate
    FIND_TARGET CMakePrivate::CMakePrivate
)

cpp_add_library(
    CMaizePrivateDepend
    SOURCE_DIR "${CMAKE_CURRENT_LIST_DIR}"
    INCLUDE_DIR "${CMAKE_CURRENT_LIST_DIR}"
    DEPENDS CMakePrivate
)

target_include_directories (CMaizePrivateDepend PUBLIC ${CMAKE_CURRENT_SOURCE_DIR})

message("Processing private depend...")
