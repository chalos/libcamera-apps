cmake_minimum_required(VERSION 3.6)

include(GNUInstallDirs)

add_library(outputs output.cpp file_output.cpp net_output.cpp circular_output.cpp)

file(GLOB HEADERS ${CMAKE_CURRENT_LIST_DIR}/*.hpp ${CMAKE_CURRENT_LIST_DIR}/*.h)
message(STATUS "HEADERS=${HEADERS}")
set_target_properties(outputs PROPERTIES PRIVATE_HEADER "${HEADERS}")

install(TARGETS outputs LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR} ARCHIVE DESTINATION ${CMAKE_INSTALL_LIBDIR}
    PRIVATE_HEADER DESTINATION "${CMAKE_INSTALL_INCLUDEDIR}/outputs"
)
