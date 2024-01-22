cmake_minimum_required(VERSION 3.16)
project(FHE-EMBED-SVM)

set(CMAKE_CXX_STANDARD 17)

# make sure you have OpenFHE v1.1.2 installed in the path below
# find_package(OpenFHE 1.1.0 EXACT REQUIRED PATHS ../../myinstalls/)
set(CMAKE_FIND_ROOT_PATH ~/development/personal/myinstalls)
find_package(OpenFHE 1.1.2 EXACT REQUIRED PATHS ~/development/personal/myinstalls/ NO_DEFAULT_PATHS)

if(NOT OpenFHE_FOUND)
    message(FATAL_ERROR "OpenFHE library not found at the specified path.")
endif()

set(CMAKE_CXX_FLAGS ${OpenFHE_CXX_FLAGS})

set(CMAKE_CXX_FLAGS_DEBUG "${CMAKE_CXX_FLAGS_DEBUG} -O0")

include_directories(${OPENMP_INCLUDES})
include_directories(${OpenFHE_INCLUDE})
include_directories(${OpenFHE_INCLUDE}/third-party/include)
include_directories(${OpenFHE_INCLUDE}/core)
include_directories(${OpenFHE_INCLUDE}/pke)
include_directories(${OpenFHE_INCLUDE}/binfhe)
link_directories(${OpenFHE_LIBDIR})
link_directories(${OPENMP_LIBRARIES})

message(STATUS "------------- Building using OpenFHE include: ${OpenFHE_INCLUDE}" )
message(STATUS "------------- Building using OpenFHE lib: ${OpenFHE_LIBDIR}" )

if (BUILD_STATIC)
    set(CMAKE_EXE_LINKER_FLAGS "${OpenFHE_EXE_LINKER_FLAGS} -static")
    link_libraries(${OpenFHE_STATIC_LIBRARIES})
else ()
    set(CMAKE_EXE_LINKER_FLAGS ${OpenFHE_EXE_LINKER_FLAGS})
    link_libraries(${OpenFHE_SHARED_LIBRARIES})
endif ()

#add_executable(svm-linear svm-linear.cpp)
#add_executable(svm-poly-v1 svm-poly-v1.cpp)
#add_executable(svm-poly-v2 svm-poly-v2.cpp)
#add_executable(svm-rbf-v1 svm-rbf-v1.cpp)
add_executable(svm-rbf svm-rbf.cpp)
#add_executable(svm-sigmoid-v1 svm-sigmoid-v1.cpp)
#add_executable(svm-sigmoid-v2 svm-sigmoid-v2.cpp)