cmake_minimum_required(VERSION 3.23)

project(AutoDoxygen VERSION 0.0.1)

include(cmake/CPM.cmake)
CPMAddPackage(
    GITHUB_REPOSITORY "jothepro/doxygen-awesome-css"
    GIT_TAG v2.3.3
)

find_package(Doxygen REQUIRED)

set(DOXYGEN_INPUT_DIR "${CMAKE_SOURCE_DIR}/Source")
set(DOXYGEN_OUTPUT_DIR "${CMAKE_BINARY_DIR}/docs/doxygen")
set(DOXYGEN_INDEX_FILE "${DOXYGEN_OUTPUT_DIR}/html/index.html")

file(MAKE_DIRECTORY ${DOXYGEN_OUTPUT_DIR})

set(DOXYFILE_IN_DIR "${CMAKE_CURRENT_SOURCE_DIR}/docs")
set(DOXYFILE_IN "${DOXYFILE_IN_DIR}/Doxyfile.in")
set(DOXYFILE_OUT "${CMAKE_CURRENT_BINARY_DIR}/Doxyfile")

configure_file("${DOXYFILE_IN}" "${DOXYFILE_OUT}" @ONLY)

file(GLOB_RECURSE ALL_HEADERS "${DOXYGEN_INPUT_DIR}/*.h")

add_custom_command(OUTPUT ${DOXYGEN_INDEX_FILE}
                   DEPENDS ${ALL_HEADERS} "${DOXYFILE_IN_DIR}/custom.css" "${DOXYFILE_IN_DIR}/header.html"
                   COMMAND ${DOXYGEN_EXECUTABLE} ${DOXYFILE_OUT}
                   MAIN_DEPENDENCY ${DOXYFILE_OUT} ${DOXYFILE_IN}
                   COMMENT "Generating docs")

add_custom_target(Doxygen ALL DEPENDS ${DOXYGEN_INDEX_FILE})
