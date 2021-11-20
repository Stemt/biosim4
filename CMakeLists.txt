
cmake_minimum_required(VERSION 3.13.4)

project(biosim4)

# OpenCV
find_package(OpenCV REQUIRED)
include_directories(${OpenCV_INCLUDE_DIRS})

# CImg
if(NOT DEFINED ${CImg_INCLUDE_DIRS})
    set(CImg_INCLUDE_DIRS ~/sources/CImg)
endif(NOT DEFINED ${CImg_INCLUDE_DIRS})

include_directories(${CImg_INCLUDE_DIRS})

# Threading
find_package(Threads REQUIRED)

find_package(X11 REQUIRED)
link_libraries(${X11_LIBRARIES})
include_directories(${X11_INCLUDE_DIR})

# output directories
make_directory(images)
make_directory(logs)



add_executable(
    biosim4
    src/analysis.cpp
    src/basicTypes.cpp
    src/createBarrier.cpp
    src/endOfGeneration.cpp
    src/endOfSimStep.cpp
    src/executeActions.cpp
    src/feedForward.cpp
    src/genome-compare.cpp
    src/genome.cpp
    src/getSensor.cpp
    src/grid.cpp
    src/imageWriter.cpp
    src/indiv.cpp
    src/main.cpp
    src/params.cpp
    src/peeps.cpp
    src/random.cpp
    src/signals.cpp
    src/simulator.cpp
    src/spawnNewGeneration.cpp
    src/survival-criteria.cpp
    src/unitTestBasicTypes.cpp
    src/unitTestConnectNeuralNetWiringFromGenome.cpp
    src/unitTestGridVisitNeighborhood.cpp
)

add_custom_command(TARGET ${PROJECT_NAME} PRE_BUILD
                   COMMAND ${CMAKE_COMMAND} -E copy_directory
                       ${CMAKE_SOURCE_DIR}/tools $<TARGET_FILE_DIR:${PROJECT_NAME}>/tools)

target_link_libraries(biosim4 ${OpenCV_LIBS} Threads::Threads)
