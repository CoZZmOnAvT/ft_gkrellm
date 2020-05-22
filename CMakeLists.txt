project(ft_gkrellm LANGUAGES CXX)

cmake_minimum_required(VERSION 3.15)

set(EXE_NAME ${PROJECT_NAME})
set(LIB_NAME ${EXE_NAME}_core)

set(CURSES_NEED_WIDE TRUE)
find_package(Curses REQUIRED)

set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} "${CMAKE_SOURCE_DIR}/cmake/")

find_package(SDL2 REQUIRED)
find_package(SDL2_image REQUIRED)
find_package(SDL2_ttf REQUIRED)

add_library(${LIB_NAME} STATIC AMonitorModule.cpp
                               DisplayContainer.cpp
                               ProcessesModule.cpp
                               ClockModule.cpp
                               HardMemModule.cpp
                               RAMMemModule.cpp
                               Cor.cpp
                               NetworkModule.cpp
                               UserDataModule.cpp
                               CpuLoadModule.cpp
                               OSInfoModule.cpp
                               VirtMemModule.cpp
                               Ncurses.cpp
                               UnicornModule.cpp
)

target_link_libraries(${LIB_NAME} PRIVATE ${CURSES_LIBRARIES}
                                          ${SDL2_LIBRARIES}
                                          ${SDL2_IMAGE_LIBRARIES}
                                          ${SDL2_TTF_LIBRARIES}
)
target_include_directories(${LIB_NAME} PRIVATE ${CURSES_INCLUDE_DIRS}
                                               ${SDL2_INCLUDE_DIRS}
                                               ${SDL2_IMAGE_INCLUDE_DIRS}
                                               ${SDL2_TTF_INCLUDE_DIRS}
)

add_executable(${EXE_NAME} main.cpp)
target_link_libraries(${EXE_NAME} PRIVATE ${LIB_NAME})
