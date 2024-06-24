cmake_minimum_required(VERSION 3.19)

project(sdlmixtest)

find_package(SDL2 CONFIG REQUIRED)
find_package(SDL2_image CONFIG REQUIRED)
find_package(SDL2_mixer CONFIG REQUIRED)

add_executable( ${PROJECT_NAME}
    example.cpp
)

if (WIN32)
    set_target_properties( ${PROJECT_NAME} PROPERTIES
      MSVC_RUNTIME_LIBRARY "MultiThreaded$<$<CONFIG:Debug>:Debug>"
    )
endif()

target_compile_definitions( ${PROJECT_NAME} PRIVATE
    MUSIC_FILE=test.mid
    SOUNDFONT_FILE=C:/ProgramData/soundfonts/default.sf2
)

target_link_libraries( ${PROJECT_NAME} PRIVATE
    SDL2::SDL2-static
    SDL2_image::SDL2_image-static
    SDL2_mixer::SDL2_mixer-static
)

configure_file(test.mid ${CMAKE_CURRENT_BINARY_DIR} COPYONLY)
configure_file(music.wav ${CMAKE_CURRENT_BINARY_DIR} COPYONLY)
configure_file(scratch.wav ${CMAKE_CURRENT_BINARY_DIR} COPYONLY)
configure_file(test.png ${CMAKE_CURRENT_BINARY_DIR} COPYONLY)
