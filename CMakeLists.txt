project(kairos)

cmake_minimum_required(VERSION 3.16)
set(CMAKE_CXX_COMPILER /usr/bin/c++)
set(CMAKE_CXX_FLAGS "-m64 -std=c++17")
add_compile_options(-W -Wall -g -fpermissive)

include(FetchContent)

FetchContent_Declare(fmt
  GIT_REPOSITORY https://github.com/fmtlib/fmt.git
  GIT_TAG        master
)

FetchContent_MakeAvailable(fmt)

include_directories(include)

###############################
# for hpp
###############################
add_library(kairos SHARED STATIC)
target_sources(kairos 
PRIVATE
    src/kairos.cpp
PUBLIC 
    include/kairos.h
)

target_include_directories (kairos
PUBLIC
    ${CMAKE_CURRENT_SOURCE_DIR}/include
    ${fmt_SOURCE_DIR}/include
)

# auto link library fmt
target_link_libraries(kairos
PUBLIC
    fmt)


