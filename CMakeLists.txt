cmake_minimum_required(VERSION 3.1)
project(imgui LANGUAGES CXX)

set(ROOT ${CMAKE_CURRENT_SOURCE_DIR})
set(IMGUI_PUBLIC_HEADERS ${ROOT}/imgui.h)
set(IMGUI_PRIVATE_HEADERS
    ${ROOT}/imgui_internal.h ${ROOT}/imconfig.h ${ROOT}/imstb_rectpack.h
    ${ROOT}/imstb_textedit.h ${ROOT}/imstb_truetype.h)
set(IMGUI_SOURCES ${ROOT}/imgui.cpp ${ROOT}/imgui_draw.cpp
                  ${ROOT}/imgui_widgets.cpp ${ROOT}/imgui_demo.cpp)

add_library(imgui_static STATIC ${IMGUI_SOURCES} ${IMGUI_PUBLIC_HEADERS}
                                ${IMGUI_PRIVATE_HEADERS})
if(BUILD_SHARED_LIBS)
  add_library(imgui_shared SHARED ${IMGUI_SOURCES})
  add_library(imgui ALIAS imgui_shared)
  target_include_directories(
    imgui_static PUBLIC $<BUILD_INTERFACE:${ROOT}>$<INSTALL_INTERFACE:imgui>)
else()
  add_library(imgui ALIAS imgui_static)
endif()
