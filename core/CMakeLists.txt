cmake_minimum_required(VERSION 3.6)

include(GNUInstallDirs)

#find_package(Boost REQUIRED COMPONENTS program_options)

find_library(Boost_program_options_LIBRARY boost_program_options PATHS "${LIBRARY_HINT}" REQUIRED)

message(STATUS "Boost_program_options library found:")
message(STATUS "    Boost_program_options_LIBRARY=${Boost_program_options_LIBRARY}")

add_custom_target(VersionCpp ${CMAKE_COMMAND} -DSOURCE_DIR=${CMAKE_SOURCE_DIR} -P ${CMAKE_CURRENT_LIST_DIR}/version.cmake)
set_source_files_properties(version.cpp PROPERTIES GENERATED 1)

add_library(libcamera_app libcamera_app.cpp post_processor.cpp version.cpp options.cpp)
add_dependencies(libcamera_app VersionCpp)

file(GLOB HEADERS ${CMAKE_CURRENT_LIST_DIR}/*.hpp ${CMAKE_CURRENT_LIST_DIR}/*.h)
message(STATUS "HEADERS=${HEADERS}")

set_target_properties(libcamera_app PROPERTIES PREFIX "" IMPORT_PREFIX "" PRIVATE_HEADER "${HEADERS}")
target_link_libraries(libcamera_app pthread preview ${LIBCAMERA_LINK_LIBRARIES} ${Boost_program_options_LIBRARY} post_processing_stages)

install(TARGETS libcamera_app LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR} ARCHIVE DESTINATION ${CMAKE_INSTALL_LIBDIR}
PRIVATE_HEADER DESTINATION "${CMAKE_INSTALL_INCLUDEDIR}/core"
)
