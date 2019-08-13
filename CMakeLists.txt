cmake_minimum_required(VERSION 3.5)
project(XDFBrowser
	LANGUAGES CXX
	VERSION 1.12.0)

set(CMAKE_AUTOMOC ON)
set(CMAKE_AUTOUIC ON)
find_package(Qt5 REQUIRED COMPONENTS Widgets)

add_executable(${PROJECT_NAME} MACOSX_BUNDLE WIN32
	main.cpp
	mainwindow.cpp
	mainwindow.h
	mainwindow.ui
	xdffile.h
	xdffile.cpp
)
target_link_libraries(${PROJECT_NAME}
	PRIVATE
	Qt5::Widgets
)

target_compile_features(${PROJECT_NAME} PRIVATE cxx_auto_type cxx_noexcept)
