CMAKE_MINIMUM_REQUIRED(VERSION 3.10)
PROJECT(IMAGE-QUILTING)

# Add the subdirectory for agz-utils and set definitions
ADD_SUBDIRECTORY(lib/my-utils)
TARGET_COMPILE_DEFINITIONS(MyUtils PUBLIC AGZ_UTILS_SSE)

# Recursively find all source and header files except the main file
FILE(GLOB_RECURSE COMMON_SRC
        "${PROJECT_SOURCE_DIR}/src/*.cpp"
        "${PROJECT_SOURCE_DIR}/include/*.h"
)

# Remove the main file from COMMON_SRC
LIST(REMOVE_ITEM COMMON_SRC "${PROJECT_SOURCE_DIR}/src/main.cpp")

# Create the executable target with main.cpp
ADD_EXECUTABLE(ImageQuilting_main ${COMMON_SRC} src/main.cpp)

# Set the C++ standard
SET_PROPERTY(TARGET ImageQuilting_main PROPERTY CXX_STANDARD 17)
SET_PROPERTY(TARGET ImageQuilting_main PROPERTY CXX_STANDARD_REQUIRED ON)

# Include directories
TARGET_INCLUDE_DIRECTORIES(ImageQuilting_main PUBLIC
        "${PROJECT_SOURCE_DIR}/lib/cxxopts"
        "${PROJECT_SOURCE_DIR}/lib/my-utils/include"
        "${PROJECT_SOURCE_DIR}/include"
)

# Link libraries
TARGET_LINK_LIBRARIES(ImageQuilting_main PUBLIC MyUtils)
