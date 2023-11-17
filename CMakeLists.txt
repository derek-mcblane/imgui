cmake_minimum_required(VERSION 3.21.0)

project(imgui
    VERSION 1.89.7
    DESCRIPTION "imgui with docking"
    HOMEPAGE_URL "https://github.com/ocornut/imgui"
)

option(IMGUI_USE_STDLIB_SUPPORT "" OFF)
option(IMGUI_DEFINE_MATH_OPERATORS "" OFF)
option(IMGUI_DISABLE "" OFF)
option(IMGUI_DISABLE_DEMO_WINDOWS "" OFF)
option(IMGUI_DISABLE_DEBUG_TOOLS "" OFF)
option(IMGUI_DISABLE_OBSOLETE_FUNCTIONS "" OFF)
option(IMGUI_DISABLE_OBSOLETE_KEYIO "" OFF)

add_library(imgui
    imconfig.h
    imgui.h
    imgui_internal.h
    imstb_rectpack.h
    imstb_textedit.h
    imstb_truetype.h
    imgui.cpp
    imgui_demo.cpp
    imgui_draw.cpp
    imgui_tables.cpp
    imgui_widgets.cpp
    $<$<BOOL:${IMGUI_USE_STDLIB_SUPPORT}>:misc/cpp/imgui_stdlib.h>
    $<$<BOOL:${IMGUI_USE_STDLIB_SUPPORT}>:misc/cpp/imgui_stdlib.cpp>
)
target_compile_features(imgui PUBLIC cxx_std_20)
target_compile_definitions(imgui PUBLIC
    $<$<BOOL:${IMGUI_DEFINE_MATH_OPERATORS}>:IMGUI_DEFINE_MATH_OPERATORS>
    $<$<BOOL:${IMGUI_DISABLE}>:IMGUI_DISABLE>
    $<$<BOOL:${IMGUI_DISABLE_DEMO_WINDOWS}>:IMGUI_DISABLE_DEMO_WINDOWS>
    $<$<BOOL:${IMGUI_DISABLE_DEBUG_TOOLS}>:IMGUI_DISABLE_DEBUG_TOOLS>
    $<$<BOOL:${IMGUI_DISABLE_OBSOLETE_FUNCTIONS}>:IMGUI_DISABLE_OBSOLETE_FUNCTIONS>
    $<$<BOOL:${IMGUI_DISABLE_OBSOLETE_KEYIO}>:IMGUI_DISABLE_OBSOLETE_KEYIO>
    $<$<BOOL:${IMGUI_USER_CONFIG}>:IMGUI_USER_CONFIG="${IMGUI_USER_CONFIG}">
)
target_include_directories(imgui PUBLIC ${CMAKE_CURRENT_LIST_DIR})
if (TARGET ${IMGUI_USER_CONFIG_TARGET})
    target_link_libraries(imgui PUBLIC ${IMGUI_USER_CONFIG_TARGET})
endif()

add_library(imgui::imgui ALIAS imgui)

add_subdirectory(backends)
