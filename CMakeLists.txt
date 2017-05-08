cmake_minimum_required (VERSION 2.8)
project (ROPTLIB C CXX)
include(CheckCXXCompilerFlag)
CHECK_CXX_COMPILER_FLAG("-std=c++14" COMPILER_SUPPORTS_CXX14)
CHECK_CXX_COMPILER_FLAG("-std=c++11" COMPILER_SUPPORTS_CXX11)
CHECK_CXX_COMPILER_FLAG("-std=c++0x" COMPILER_SUPPORTS_CXX0X)
if(COMPILER_SUPPORTS_CXX14)
  set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++14 -pthread")
elseif(COMPILER_SUPPORTS_CXX11)
  set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11 -pthread")
elseif(COMPILER_SUPPORTS_CXX0X)
  set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++0x")
else()
  message(STATUS "The compiler ${CMAKE_CXX_COMPILER} has no C++11 support. Please use a different C++ compiler.")
endif()
find_package(LAPACK REQUIRED)
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Fno-strict-aliasing")
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wno-misleading-indentation")
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wno-deprecated-declarations")
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wno-multichar")
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wno-ignored-attributes")
set(EIGEN_DIR ${PROJECT_SOURCE_DIR}/../libigl/external/nanogui/ext/eigen)
set(MANIFOLD_DIR ${PROJECT_SOURCE_DIR}/Manifolds)
set(PROBLEM_DIR ${PROJECT_SOURCE_DIR}/Problems)
set(OTHERS_DIR ${PROJECT_SOURCE_DIR}/Others)
set(SOLVERS_DIR ${PROJECT_SOURCE_DIR}/Solvers)
set(SRC_DIR ${PROJECT_SOURCE_DIR}/src)
include_directories(
  ${EIGEN_DIR}
  ${MANIFOLD_DIR}
  ${MANIFOLD_DIR}/Euclidean/
  ${MANIFOLD_DIR}/OrthGroup/
  ${MANIFOLD_DIR}/Sphere/
  ${MANIFOLD_DIR}/Stiefel/
  ${OTHERS_DIR}
  ${PROBLEM_DIR}
  ${PROBLEM_DIR}/SphereConvexHull/
  ${SOLVERS_DIR}
  ${SRC_DIR}
  ${PROJECT_SOURCE_DIR}
  ${PROJECT_SOURCE_DIR}/cwrapper/blas/
  ${PROJECT_SOURCE_DIR}/cwrapper/lapack/
  )
set(SOURCES
  ${MANIFOLD_DIR}/Element.cpp
  ${MANIFOLD_DIR}/LinearOPE.cpp
  ${MANIFOLD_DIR}/Manifold.cpp
  ${MANIFOLD_DIR}/ProductElement.cpp
  ${MANIFOLD_DIR}/ProductManifold.cpp
  ${MANIFOLD_DIR}/SharedSpace.cpp
  ${MANIFOLD_DIR}/SmartSpace.cpp
  ${MANIFOLD_DIR}/Euclidean/EucVariable.cpp
  ${MANIFOLD_DIR}/Euclidean/EucVector.cpp
  ${MANIFOLD_DIR}/Euclidean/Euclidean.cpp
  ${MANIFOLD_DIR}/Sphere/Sphere.cpp
  ${MANIFOLD_DIR}/Sphere/SphereVariable.cpp
  ${MANIFOLD_DIR}/Sphere/SphereVector.cpp
  ${MANIFOLD_DIR}/Stiefel/StieVariable.cpp
  ${MANIFOLD_DIR}/Stiefel/StieVector.cpp
  ${MANIFOLD_DIR}/Stiefel/Stiefel.cpp
  ${MANIFOLD_DIR}/OrthGroup/OrthGroup.cpp
  ${MANIFOLD_DIR}/OrthGroup/OrthGroupVariable.cpp
  ${MANIFOLD_DIR}/OrthGroup/OrthGroupVector.cpp
  ${OTHERS_DIR}/MinPNormConHull.cpp
  ${OTHERS_DIR}/MyMatrix.cpp
  ${OTHERS_DIR}/Timer.cpp
  ${OTHERS_DIR}/randgen.cpp
  ${SOLVERS_DIR}/Solvers.cpp
  ${SOLVERS_DIR}/QuasiNewton.cpp
  ${SOLVERS_DIR}/SolversTR.cpp
  ${SOLVERS_DIR}/RTRNewton.cpp
  ${PROBLEM_DIR}/Problem.cpp
  ${PROBLEM_DIR}/SphereConvexHull/SphereConvexHull.cpp
)
add_library(ROPTLIB ${SOURCES})
target_link_libraries(ROPTLIB  ${LAPACK_LIBRARIES})
