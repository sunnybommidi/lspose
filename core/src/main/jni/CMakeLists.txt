project(core)
cmake_minimum_required(VERSION 3.4.1)

add_subdirectory(${EXTERNAL_ROOT} external)

configure_file(template/config.cpp src/config.cpp)

aux_source_directory(src SRC_LIST)
aux_source_directory(src/jni SRC_LIST)

add_library(${PROJECT_NAME} STATIC ${SRC_LIST} ${CMAKE_CURRENT_BINARY_DIR}/src/config.cpp)

target_include_directories(${PROJECT_NAME} PUBLIC include)
target_include_directories(${PROJECT_NAME} PRIVATE src)

target_link_libraries(${PROJECT_NAME} PUBLIC dobby lsplant_static log fmt-header-only)
target_link_libraries(${PROJECT_NAME} PRIVATE dex_builder_static)
