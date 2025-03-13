cmake_minimum_required(VERSION 3.10)
project(libpqtypes C)

# Find PostgreSQL
find_package(PostgreSQL REQUIRED)
include_directories(${PostgreSQL_INCLUDE_DIRS})

# Define source files
set(SRC_FILES
    src/array.c src/datetime.c src/error.c
    src/events.c src/exec.c src/geo.c src/handler.c
    src/misc.c src/network.c src/numerics.c
    src/param.c src/port.c src/record.c src/spec.c
    src/utils.c src/varlena.c
)

# Define the library
add_library(${PROJECT_NAME} SHARED ${SRC_FILES})
target_link_libraries(${PROJECT_NAME} ${PostgreSQL_LIBRARIES})

# Set compiler flags
if(MSVC)
    target_compile_definitions(${PROJECT_NAME} PRIVATE _WIN32_WINNT=0x0501 _CRT_SECURE_NO_WARNINGS _USE_MATH_DEFINES)
    target_compile_options(${PROJECT_NAME} PRIVATE /W4 /MD /GF /Ob2)
    if(CMAKE_BUILD_TYPE STREQUAL "Release")
        target_compile_options(${PROJECT_NAME} PRIVATE /O2)
    endif()
    # Ensure linking with ws2_32.lib for networking functions like htonl
    target_link_libraries(${PROJECT_NAME} ws2_32)
else()
    target_compile_options(${PROJECT_NAME} PRIVATE -Wall -Wextra -O2 -fPIC)
    target_link_libraries(${PROJECT_NAME} m) # Link math library
endif()

# Install targets
install(TARGETS ${PROJECT_NAME} LIBRARY DESTINATION lib ARCHIVE DESTINATION lib RUNTIME DESTINATION bin)
install(DIRECTORY include/ DESTINATION include)
