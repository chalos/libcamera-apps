cmake_minimum_required(VERSION 3.6)

include(GNUInstallDirs)

add_library(encoders encoder.cpp null_encoder.cpp h264_encoder.cpp mjpeg_encoder.cpp)
target_link_libraries(encoders jpeg)

file(GLOB HEADERS ${CMAKE_CURRENT_LIST_DIR}/*.hpp ${CMAKE_CURRENT_LIST_DIR}/*.h)
message(STATUS "HEADERS=${HEADERS}")
set_target_properties(encoders PROPERTIES PRIVATE_HEADER "${HEADERS}")

install(TARGETS encoders LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR} ARCHIVE DESTINATION ${CMAKE_INSTALL_LIBDIR}
    PRIVATE_HEADER DESTINATION "${CMAKE_INSTALL_INCLUDEDIR}/encoder"
)
