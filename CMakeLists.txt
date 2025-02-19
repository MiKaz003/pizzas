cmake_minimum_required(VERSION 3.11.0)
project(Pizzas)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

set(SRC_LIST
    src/Funghi.cpp
    src/Margherita.cpp
    src/Pizza.cpp
    src/Pizzeria.cpp)

add_library(${PROJECT_NAME}-lib STATIC ${SRC_LIST})
set_target_properties(${PROJECT_NAME}-lib PROPERTIES PREFIX "")

add_executable(${PROJECT_NAME} ${SRC_LIST} src/main.cpp)
target_link_libraries(${PROJECT_NAME} PRIVATE ${PROJECT_NAME}-lib)
target_link_libraries(${PROJECT_NAME} PRIVATE pthread)

enable_testing()
include(FetchContent)
FetchContent_Declare(
  googletest
  URL https://github.com/google/googletest/archive/03597a01ee50ed33e9dfd640b249b4be3799d395.zip
)

add_executable(${PROJECT_NAME}-ut ${SRC_LIST} test/PizzeriaTest.cpp)
add_test(NAME Test Command ${PROJECT_NAME}-ut)
# TODO: Write proper build system :)
