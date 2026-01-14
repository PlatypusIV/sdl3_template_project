cmake_minimum_required(VERSION 3.28)

#change template to suit project
project (template)

add_executable(
    template
    src/main.cpp
)

target_include_directories(
    template
    PRIVATE
    include
)

target_link_directories(
    template
    PRIVATE
    lib
)

target_link_libraries(
    template
    PRIVATE
    SDL3
)

# Copy SDL3.dll to the build directory after building (Windows only)
if(WIN32)
    add_custom_command(TARGET template POST_BUILD
        COMMAND ${CMAKE_COMMAND} -E copy_if_different
        "${CMAKE_SOURCE_DIR}/bin/SDL3.dll"
        $<TARGET_FILE_DIR:template>
    )
endif()