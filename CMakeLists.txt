cmake_minimum_required(VERSION 3.22)
project(actions_test)

set(CMAKE_CXX_STANDARD 14)

add_executable(actions_test main.cpp)

find_package(Python COMPONENTS Interpreter)

if (Python_FOUND)
    message("Default python interpreter: ${Python_EXECUTABLE}")
    set(venv ${CMAKE_BINARY_DIR}/.venv)

    if (NOT EXISTS ${venv})
        message("Creating virtual environment at ${venv}")
        execute_process(COMMAND ${Python_EXECUTABLE} -m venv ${venv})
    endif()

    # A trick to make sure cmake uses the virtual environment we've created
    set(ENV{VIRTUAL_ENV} ${venv})
    set(Python_FIND_VIRTUALENV ONLY)
    unset (Python_EXECUTABLE)
    find_package(Python COMPONENTS Interpreter)

    message("Python interpreter: ${Python_EXECUTABLE}")
endif()