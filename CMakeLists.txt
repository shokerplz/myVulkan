cmake_minimum_required(VERSION 3.10)
project(myVulkan)

# Let CMake use our C++17 or higher standard
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# On macOS, we need to use the metal extension
add_definitions(-DVK_USE_PLATFORM_METAL_EXT)

# Find Vulkan (comes from the Vulkan SDK)
find_package(Vulkan REQUIRED)

# Find GLFW (installed via brew)
find_package(PkgConfig REQUIRED)
pkg_search_module(GLFW REQUIRED glfw3)

pkg_search_module(GLM REQUIRED glm)

# Or use the CMake config if available:
# find_package(GLFW3 REQUIRED)

# For convenience, add include directories
include_directories(
    ${Vulkan_INCLUDE_DIR}
    ${GLFW_INCLUDE_DIRS}
    ${GLM_INCLUDE_DIRS}
)

# Source files
set(SOURCES
    main.cpp
)

add_executable(${PROJECT_NAME} ${SOURCES})

# Link with Vulkan and GLFW
target_link_libraries(${PROJECT_NAME}
    ${Vulkan_LIBRARIES}
    ${GLM_LIBRARIES}
)

find_library(MOLTENVK MoltenVK
  PATHS
    "/Users/admin/VulkanSDK/1.4.304.0/macOS/lib"
  PATH_SUFFIXES "."
)

find_library(GLFW_LIBRARY glfw
  PATHS
    "/opt/homebrew/Cellar/glfw/3.4/lib/"
  PATH_SUFFIXES "."
)

target_link_libraries(${PROJECT_NAME} 
    ${MOLTENVK}
    ${GLFW_LIBRARY}
)