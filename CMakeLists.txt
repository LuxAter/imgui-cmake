cmake_minimum_required(VERSION 3.1)
project(imgui LANGUAGES CXX)

set(IMGUI_PUBLIC_HEADERS imgui.h)
set(IMGUI_PRIVATE_HEADERS imgui_internal.h imgui_config.h imstb_rectpack.h
                          imstb_textedit.h imstb_truetype.h)
set(IMGUI_SOURCES imgui.cpp imgui_draw.cpp imgui_widgets.cpp imgui_demo.cpp)

add_library(imgui_static STATIC ${IMGUI_SOURCES} ${IMGUI_PUBLIC_HEADERS} ${IMGUI_PRIVATE_HEADERS})
if(BUILD_SHARED_LIBS)
  add_library(imgui_shared SHARED ${IMGUI_SOURCES})
  add_library(imgui ALIAS imgui_shared)
  target_include_directories(imgui_static PUBLIC $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}>$<INSTALL_INTERFACE:imgui>)
else()
  add_library(imgui ALIAS imgui_static)
endif()
