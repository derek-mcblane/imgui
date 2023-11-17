find_package(SDL2 REQUIRED COMPONENTS SDL2)

# SDL2 Backend
add_library(SDL2Backend
    imgui_impl_sdl2.h
    imgui_impl_sdl2.cpp
)
target_compile_features(SDL2Backend PUBLIC cxx_std_20)
target_include_directories(SDL2Backend PUBLIC ${CMAKE_CURRENT_LIST_DIR})
target_link_libraries(SDL2Backend
PRIVATE
    imgui
    SDL2::SDL2
)

add_library(imgui::SDL2Backend ALIAS SDL2Backend)

# SDL2 Renderer Backend
add_library(SDL2RendererBackend
    imgui_impl_sdlrenderer2.h
    imgui_impl_sdlrenderer2.cpp
)
target_compile_features(SDL2RendererBackend PUBLIC cxx_std_20)
target_include_directories(SDL2RendererBackend PUBLIC ${CMAKE_CURRENT_LIST_DIR})
target_link_libraries(SDL2RendererBackend
PRIVATE
    imgui
    SDL2::SDL2
)

add_library(imgui::SDL2RendererBackend ALIAS SDL2RendererBackend)
