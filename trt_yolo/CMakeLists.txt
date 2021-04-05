cmake_minimum_required(VERSION 2.8.3)
project(trt_yolo)

find_package(catkin REQUIRED
  COMPONENTS
)

find_package(CUDA REQUIRED)

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11 -Wall -Ofast -Wfatal-errors -D_MWAITXINTRIN_H_INCLUDED")
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}/lib)

include_directories(
  include
  ${catkin_INCLUDE_DIRS}
)

cuda_add_library(${PROJECT_NAME} SHARED src/trt_yolo/yolo_layer.cu)
target_link_libraries(${PROJECT_NAME} ${CUDA_LIBRARIES})

add_definitions(-O2 -pthread)

catkin_package()

# catkin_install_python(
#   PROGRAMS
#     scripts/node.py
#   DESTINATION
#     ${CATKIN_PACKAGE_BIN_DESTINATION}
# )

catkin_python_setup()

