cmake_minimum_required(VERSION 3.21)

project(clang-tool-example)

find_package(LLVM REQUIRED)
find_package(Clang REQUIRED)

execute_process (
    COMMAND bash -c "${LLVM_DIR}/bin/clang++ -E -x c++ - -v < /dev/null 2>&1 | grep \"lib/clang\" | awk '{{print $1}}' | grep include"
    OUTPUT_VARIABLE CLANG_BUILTIN_INCLUDE_DIR
)

message(STATUS "CLANG_BUILTIN_INCLUDE_DIR = ${CLANG_BUILTIN_INCLUDE_DIR}")

file(WRITE "${CMAKE_CURRENT_BINARY_DIR}/bin/builtInInclude.path" "${CLANG_BUILTIN_INCLUDE_DIR}")

list(APPEND CMAKE_MODULE_PATH "${CMAKE_CURRENT_LIST_DIR}/cmake")

add_subdirectory(src)
