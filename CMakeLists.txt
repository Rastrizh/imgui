cmake_minimum_required(VERSION 3.6...3.7)

project(ImGUI CXX)

# Source groups
set(Common_sources
    "imconfig.h"
    "imgui.h"
    "imgui.cpp"
    "imgui_draw.cpp"
    "imgui_internal.h"
    "imgui_tables.cpp"
    "imgui_widgets.cpp"
    "imstb_rectpack.h"
    "imstb_textedit.h"
    "imstb_truetype.h"
    "imgui_demo.cpp"
    #"misc/debugger/imgui.natvis"
    #"misc/debugger/imgui.natstepfilter"
    "misc/cpp/imgui_stdlib.h"
    "misc/cpp/imgui_stdlib.cpp"
)
set(DX11_SOURCES
    "backends/imgui_impl_win32.h"
    "backends/imgui_impl_win32.cpp"
    "backends/imgui_impl_dx11.h"
    "backends/imgui_impl_dx11.cpp"
)
set(GLFW_SOURCES
    "backends/imgui_impl_glfw.h"
    "backends/imgui_impl_glfw.cpp"
    "backends/imgui_impl_opengl3.h"
    "backends/imgui_impl_opengl3.cpp"
)


if(RENDER_OPEN_GL)
set(ALL_FILES
    ${Common_sources}
    ${GLFW_SOURCES}
)
elseif(RENDER_D3D11)
set(ALL_FILES
    ${Common_sources}
    ${DX11_SOURCES}
)
endif()

source_group("Source Files" FILES ${ALL_FILES})

add_library(${PROJECT_NAME} STATIC ${ALL_FILES})

# Include directories
target_include_directories(${PROJECT_NAME} PUBLIC
    ${CMAKE_CURRENT_SOURCE_DIR}
)

target_compile_features(${PROJECT_NAME} PUBLIC cxx_std_20)

# Compile and link options
target_compile_options(${PROJECT_NAME} PUBLIC
    $<$<CONFIG:Debug>:/Od /Zi /MDd /EHsc>
    $<$<CONFIG:Release>:/O2 /Oi /Gy /MD /EHsc>
    /permissive-;
    ${DEFAULT_CXX_DEBUG_INFORMATION_FORMAT};
)
target_link_options(engine_compiler_flags INTERFACE
    $<$<CONFIG:Release>:/OPT:REF; /OPT:ICF>
    /DEBUG:FULL;
)
