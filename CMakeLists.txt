cmake_minimum_required(VERSION 3.16)
project(XDFBrowser
	LANGUAGES CXX
	VERSION 1.13.1)

set(CMAKE_AUTOMOC ON)
set(CMAKE_AUTOUIC ON)
find_package(Qt6 REQUIRED COMPONENTS Widgets)

qt_add_executable(${PROJECT_NAME} WIN32 MACOSX_BUNDLE
	main.cpp
	mainwindow.cpp
	mainwindow.h
	mainwindow.ui
	xdffile.h
	xdffile.cpp
)
target_link_libraries(${PROJECT_NAME} PRIVATE Qt6::Widgets)

target_compile_features(${PROJECT_NAME} PRIVATE cxx_auto_type cxx_noexcept)

install(TARGETS ${PROJECT_NAME}
	RUNTIME DESTINATION .
	BUNDLE  DESTINATION .
)
