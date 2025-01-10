cmake_minimum_required(VERSION 3.22)

project(battle_game)
set(CMAKE_CXX_STANDARD 17)

if (MSVC)
    add_compile_options(/utf-8)
endif()

set(BATTLE_GAME_ASSETS_DIR ${CMAKE_CURRENT_SOURCE_DIR}/assets)

# 设置 vcpkg 工具链文件
if(DEFINED ENV{VCPKG_ROOT} AND NOT DEFINED CMAKE_TOOLCHAIN_FILE)
    set(CMAKE_TOOLCHAIN_FILE "$ENV{VCPKG_ROOT}/scripts/buildsystems/vcpkg.cmake" CACHE STRING "")
endif()

add_subdirectory(external/grassland)
find_package(absl CONFIG REQUIRED)
find_package(glm CONFIG REQUIRED)  # 添加对 glm 的查找

list(APPEND BATTLE_GAME_EXTERNAL_INCLUDE_DIRS ${CMAKE_CURRENT_SOURCE_DIR}/external/abseil-cpp)
list(APPEND BATTLE_GAME_EXTERNAL_INCLUDE_DIRS ${GRASSLAND_INCLUDE_DIRS})

add_subdirectory(src)

target_compile_definitions(battle_game PRIVATE BATTLE_GAME_ASSETS_DIR="${BATTLE_GAME_ASSETS_DIR}/")
