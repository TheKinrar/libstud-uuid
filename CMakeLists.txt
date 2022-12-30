cmake_minimum_required(VERSION 3.24)
project(stud-uuid VERSION 1.0.6)
set(CMAKE_CXX_STANDARD 14)

add_library(stud-uuid STATIC
        libstud/uuid/uuid.cxx libstud/uuid/uuid.hxx
        libstud/uuid/uuid-io.cxx libstud/uuid/uuid-io.hxx
        libstud/uuid/version.hxx)

if(WIN32)
    target_sources(stud-uuid PRIVATE libstud/uuid/uuid-windows.cxx)
    target_link_libraries(stud-uuid rpcrt4.lib)
elseif(UNIX)
    target_sources(stud-uuid PRIVATE libstud/uuid/uuid-linux.cxx)
else()
    message(FATAL_ERROR "Target platform is not supported.")
endif()

target_include_directories(stud-uuid PUBLIC ${CMAKE_CURRENT_SOURCE_DIR})
set_target_properties(stud-uuid PROPERTIES LINKER_LANGUAGE CXX)
set_target_properties(stud-uuid PROPERTIES VERSION ${PROJECT_VERSION})
