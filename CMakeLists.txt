cmake_minimum_required(VERSION 3.22)
project(actions_test)

set(CMAKE_CXX_STANDARD 14)

add_executable(actions_test main.cpp)

message("Python venv: $ENV{PYTHON_VENV}")

find_package(Python COMPONENTS Interpreter REQUIRED)
message("Default python interpreter: ${Python_EXECUTABLE}")

if ($ENV{PYTHON_VENV} STREQUAL "")
    set(venv ${CMAKE_SOURCE_DIR}/.venv)
    message("Creating virtual environment at ${venv}")
    execute_process(COMMAND ${Python_EXECUTABLE} -m venv ${venv})
else()
    set(venv $ENV{PYTHON_VENV})
    set(Python_ROOT_DIR ${venv}/Scripts)
endif()

message("Using Python virtual environment: ${venv}")
unset (Python_EXECUTABLE)
set(Python_ROOT_DIR ${venv}/Scripts)
find_package(Python COMPONENTS Interpreter REQUIRED)

message("Python interpreter: ${Python_EXECUTABLE}")