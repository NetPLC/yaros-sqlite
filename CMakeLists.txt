# project sqlite library

project(sqlite3)

cmake_minimum_required(VERSION 2.6)

message(STATUS "operation system is ${CMAKE_SYSTEM}")

set(sqlite_srcs
	sqlite3.c)

set(shell_srcs
        shell.c)

# generate library
add_library(sqlite ${sqlite_srcs})
add_executable(sqlite3 ${shell_srcs})

if (WIN32)
    target_link_libraries(sqlite3 sqlite)
elseif (UNIX)
    target_link_libraries(sqlite3 sqlite dl pthread)
endif()


# install library
install(TARGETS sqlite3 sqlite
        RUNTIME DESTINATION bin
	LIBRARY DESTINATION lib
	ARCHIVE DESTINATION lib)

# install header
install(FILES sqlite3.h sqlite3ext.h DESTINATION include)
