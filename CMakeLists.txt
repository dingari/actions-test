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
#    set(ENV{VIRTUAL_ENV} ${venv})
    unset (Python_EXECUTABLE)
#    set(Python_FIND_VIRTUALENV ONLY)
    set(Python_ROOT_DIR ${venv}/Scripts)
    find_package(Python COMPONENTS Interpreter REQUIRED)

    message("Python interpreter: ${Python_EXECUTABLE}")
endif()