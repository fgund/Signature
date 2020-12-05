cmake_minimum_required(VERSION 3.2)

include(${CMAKE_BINARY_DIR}/conanbuildinfo.cmake) 
conan_basic_setup(TARGETS)

project(signature_cli)
add_executable(${PROJECT_NAME} main.cpp)

set_target_properties(
	${PROJECT_NAME}
PROPERTIES
    CXX_STANDARD 17
    CXX_STANDARD_REQUIRED ON
)
target_link_libraries(${PROJECT_NAME}
    CONAN_PKG::boost_crc
)

if (MSVC)
    target_compile_options(${PROJECT_NAME} PRIVATE
        /W4 /MD
    )
else ()
    find_package(Threads REQUIRED)
    target_link_libraries(${PROJECT_NAME} Threads::Threads)
    target_compile_options(${PROJECT_NAME} PRIVATE
        -Wall -Wextra -pedantic -Werror
    )
endif()
