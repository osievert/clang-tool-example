cmake_minimum_required(VERSION 3.21)

set(CMAKE_CXX_FLAGS "-Wall -g3 -O0 -fno-rtti ${LLVM_COMPILE_FLAGS}")

# include_directories(${LLVM_INCLUDE_DIRS})
# include_directories(${CLANG_INCLUDE_DIRS})

# string(STRIP ${LLVM_LDFLAGS} LLVM_LDFLAGS) # remove trailing whitespace

message(STATUS "LLVM_COMPILE_FLAGS = ${LLVM_COMPILE_FLAGS}")
# message(STATUS "CLANG_LIBS = ${CLANG_LIBS}")
# message(STATUS "LLVM_LIBS_CORE = ${LLVM_LIBS_CORE}")
# message(STATUS "LLVM_LDFLAGS = ${LLVM_LDFLAGS}")

add_executable(clang-tool main.cpp)

# target_link_directories(otto PUBLIC /opt/homebrew/Cellar/zstd/1.5.5/lib)
target_include_directories(clang-tool PRIVATE ${LLVM_INCLUDE_DIRS} ${CLANG_INCLUDE_DIRS})
target_link_directories(clang-tool PRIVATE ${ZSTD_DIR})
target_link_libraries(clang-tool ${CLANG_LIBS} ${LLVM_LIBS_CORE} ${LLVM_LDFLAGS})
