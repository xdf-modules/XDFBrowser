cmake_minimum_required(VERSION 3.5)
project(XDFBrowser
	LANGUAGES CXX
	VERSION 1.13.1)

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

if (WIN32)
	get_target_property(QT5_QMAKE_EXECUTABLE Qt5::qmake IMPORTED_LOCATION)
	get_filename_component(QT5_WINDEPLOYQT_EXECUTABLE ${QT5_QMAKE_EXECUTABLE} PATH)
	set(QT5_WINDEPLOYQT_EXECUTABLE "${QT5_WINDEPLOYQT_EXECUTABLE}/windeployqt.exe")

	add_custom_command(
		TARGET ${PROJECT_NAME} POST_BUILD
		COMMAND ${QT5_WINDEPLOYQT_EXECUTABLE} --qmldir
			${CMAKE_SOURCE_DIR} $<TARGET_FILE_DIR:${PROJECT_NAME}>)
endif(WIN32)
