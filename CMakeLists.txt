cmake_minimum_required(VERSION 3.1)

project(ImGUI CXX)

# Source groups
set(Source_Files
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
)
source_group("Source Files" FILES ${Source_Files})

set(ALL_FILES
    ${Source_Files}
)

add_library(${PROJECT_NAME} STATIC ${ALL_FILES})

target_compile_features(${PROJECT_NAME} PUBLIC cxx_std_17)
