cmake_minimum_required(VERSION 3.10)
project(Vcpkg-Project-Example VERSION 0.1.0 LANGUAGES C CXX)

include(CTest)
enable_testing()

set(src
        ${CMAKE_CURRENT_SOURCE_DIR}/src/main.cpp
)

add_definitions(-DASSETS_DIR="${CMAKE_SOURCE_DIR}/assets")

include_directories(${CMAKE_CURRENT_SOURCE_DIR})

find_package(SDL2 REQUIRED)
find_package(SDL2_image REQUIRED)
find_package(SDL2_mixer REQUIRED)

include_directories(Vcpkg-Project-Example ${SDL2_INCLUDE_DIRS} ${SDL2_IMAGE_INCLUDE_DIRS} ${SDL2_MIXER_INCLUDE_DIRS})

add_executable(Vcpkg-Project-Example ${src})

target_link_libraries(Vcpkg-Project-Example PRIVATE SDL2::SDL2)

if(TARGET SDL2_image::SDL2_image)
  target_link_libraries(Vcpkg-Project-Example PRIVATE SDL2_image::SDL2_image)
else()
  target_link_libraries(Vcpkg-Project-Examplein PRIVATE SDL2_image::SDL2_image-static)
endif()

if(TARGET SDL2_mixer::SDL2_mixer)
  target_link_libraries(Vcpkg-Project-Example PRIVATE SDL2_mixer::SDL2_mixer)
else()
  target_link_libraries(maVcpkg-Project-Examplein PRIVATE SDL2_mixer::SDL2_mixer-static)
endif()

set(CPACK_PROJECT_NAME ${PROJECT_NAME})
set(CPACK_PROJECT_VERSION ${PROJECT_VERSION})
include(CPack)