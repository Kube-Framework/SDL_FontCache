cmake_minimum_required(VERSION 3.21)
project(SDL_FontCache VERSION 0.10.0 LANGUAGES C)

find_package(SDL2 REQUIRED)
find_package(SDL2-ttf REQUIRED)

add_library(FontCache
    SDL2/SDL_FontCache.h
    SDL2/SDL_FontCache.c
)
add_library(SDL2::SDL2_FontCache ALIAS FontCache)


target_include_directories(FontCache PUBLIC .)

target_link_libraries(FontCache
    PUBLIC
        SDL2::SDL2-static
        SDL2::SDL2_ttf
)

if (FC_TESTS)
    add_executable(FontCache-tests
        test/main.c
    )
    file(COPY test/utf8_sample.txt DESTINATION ${CMAKE_BINARY_DIR})
    file(COPY test/fonts/FreeSans.ttf DESTINATION ${CMAKE_BINARY_DIR}/fonts)
    target_link_libraries(FontCache-tests SDL2::SDL2_FontCache)
endif()

