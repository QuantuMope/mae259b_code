cmake_minimum_required(VERSION 3.11)
project(KnotTyingIMC)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_BUILD_TYPE Release)
set(CMAKE_CXX_FLAGS "-Wno-deprecated-declarations -fopenmp")
set(CMAKE_CXX_FLAGS_RELEASE "-O3")
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY "../")

list(APPEND CMAKE_MODULE_PATH ${CMAKE_CURRENT_SOURCE_DIR}/cmake/modules)

find_package(SymEngine REQUIRED)
find_package(Eigen3 3.4 REQUIRED)
find_package(OpenGL REQUIRED)
find_package(GLUT REQUIRED)
find_package(MKL REQUIRED)

include_directories(${SYMENGINE_INCLUDE_DIRS}
        ${EIGEN_INCLUDE_DIRS}
        ${OPENGL_INCLUDE_DIRS}
        ${GLUT_INCLUDE_DIRS}
        ${MKL_INCLUDE_DIR})

link_directories(${MKL_LIBRARY_DIR})

add_executable(simDER
        src/main.cpp
        src/world.cpp
        src/elasticRod.cpp
        src/elasticStretchingForce.cpp
        src/elasticBendingForce.cpp
        src/elasticTwistingForce.cpp
        src/externalGravityForce.cpp
        src/dampingForce.cpp
        src/inertialForce.cpp
        src/timeStepper.cpp
        src/setInput.cpp
        src/symbolicEquations.cpp
        src/collisionDetector.cpp
        src/contactPotentialIMC.cpp)

target_link_libraries(simDER
        ${SYMENGINE_LIBRARIES}
        ${OPENGL_LIBRARIES}
        ${GLUT_LIBRARIES}
        ${MKL_LIBRARIES}
        Eigen3::Eigen
        lapack
        gfortran
        pthread
        rt
        m)
