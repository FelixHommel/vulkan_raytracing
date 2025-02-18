cmake_minimum_required(VERSION 3.30)
project(
    Template
    DESCRIPTION "Basic C++ template"
    LANGUAGES CXX
)

find_program(CLANG_FORMAT NAMES clang-format)
if(CLANG_FORMAT)
    file(GLOB_RECURSE SOURCE_FILES
        ${PROJECT_SOURCE_DIR}/src/*.cpp
        ${PROJECT_SOURCE_DIR}/src/*.hpp
    )

    add_custom_target(
        format
        COMMAND ${CLANG_FORMAT} -i ${SOURCE_FILES} --style=file:${CMAKE_SOURCE_DIR}/.clang-format
        COMMENT "Run clang-format on all source and header files"
    )
endif()

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

include(cmake/DefaultProjectSettings.cmake)

add_library(project_warnings INTERFACE)
include(cmake/CompilerWarnings.cmake)
set_project_warnings(project_warnings)

enable_testing()

add_subdirectory(deps)
add_subdirectory(src)
