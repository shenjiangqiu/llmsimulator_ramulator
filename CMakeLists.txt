#### Prompt the build type ####
if(NOT CMAKE_BUILD_TYPE)
  set(CMAKE_BUILD_TYPE "Release" CACHE STRING "" FORCE)
endif()
message("Configuring ${CMAKE_PROJECT_NAME} ${CMAKE_PROJECT_Version}...")
message(STATUS "Build type: ${CMAKE_BUILD_TYPE}")
set(CMAKE_CXX_FLAGS_DEBUG "${CMAKE_CXX_FLAGS_DEBUG} -DRAMULATOR_DEBUG")
# set(CMAKE_CXX_FLAGS_RELEASE "${CMAKE_CXX_FLAGS_RELEASE}")
set(CMAKE_POSITION_INDEPENDENT_CODE ON)
###############################

set(CMAKE_EXPORT_COMPILE_COMMANDS ON CACHE INTERNAL "")

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED True)
set(CMAKE_CXX_EXTENSIONS OFF)

include_directories(${CMAKE_CURRENT_SOURCE_DIR}/src)

#add_compile_options(-ggdb)

# add_library(ramulator SHARED)

# target_sources(ramulator 
# PRIVATE src/main.cpp)

# set_target_properties(ramulator PROPERTIES
#   #LIBRARY_OUTPUT_DIRECTORY  ${PROJECT_SOURCE_DIR}
#   LIBRARY_OUTPUT_DIRECTORY  ${CMAKE_BINARY_DIR}
# )

# target_link_libraries(
#   ramulator
#   PRIVATE yaml-cpp
#   PRIVATE spdlog
#   PRIVATE argparse
# )

# target_link_libraries(
#   llm_system
#   PRIVATE yaml-cpp
#   PRIVATE spdlog
#   PRIVATE argparse
# )
target_link_libraries(
  dram
  PUBLIC yaml-cpp
  PUBLIC spdlog
  PUBLIC argparse
)

# add_executable(ramulator-exe)
# target_link_libraries(
#   ramulator-exe 
#   PRIVATE ramulator
#   PRIVATE argparse
# )

# set_target_properties(
#   ramulator-exe
#   PROPERTIES 
#   OUTPUT_NAME ramulator2
#   RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}
# )

target_include_directories(
  hardware
  PUBLIC src
  PUBLIC ${spdlog_SOURCE_DIR}/include
  PUBLIC ${yaml-cpp_SOURCE_DIR}/include
  PUBLIC ${argparse_SOURCE_DIR}/include
)

target_include_directories(
  llm_system
  PUBLIC src
  PUBLIC ${spdlog_SOURCE_DIR}/include
  PUBLIC ${yaml-cpp_SOURCE_DIR}/include
  PUBLIC ${argparse_SOURCE_DIR}/include
)


target_include_directories(
  dram 
  PUBLIC src
  PUBLIC ${spdlog_SOURCE_DIR}/include
  PUBLIC ${yaml-cpp_SOURCE_DIR}/include
  PUBLIC ${argparse_SOURCE_DIR}/include
)

add_subdirectory(src)
