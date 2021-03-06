
find_package(Doxygen REQUIRED)

# set the input and output documentation paths
set(DOXYGEN_INPUT_DIR ${PROJECT_SOURCE_DIR})
set(DOXYGEN_OUTPUT_DIR ${PROJECT_BINARY_DIR}/doxygen)

# configure the source LocalDoxyfile by copying it and replacing all @variables@
set(DOXYGEN_CONFIGURED_INPUT ${DOXYGEN_OUTPUT_DIR}/LocalDoxyfile)
configure_file(${DOXYGEN_INPUT_DIR}/doxygen/LocalDoxyfile ${DOXYGEN_CONFIGURED_INPUT} @ONLY)

# copy the files needed by the documentation
configure_file(${DOXYGEN_INPUT_DIR}/doxygen/doxygen.css ${DOXYGEN_OUTPUT_DIR}/doxygen.css COPYONLY)
configure_file(${DOXYGEN_INPUT_DIR}/doxygen/footer_helper.css ${DOXYGEN_OUTPUT_DIR}/footer_helper.css COPYONLY)
configure_file(${DOXYGEN_INPUT_DIR}/doxygen/main_additions.css ${DOXYGEN_OUTPUT_DIR}/main_additions.css COPYONLY)
configure_file(${DOXYGEN_INPUT_DIR}/doxygen/main.css ${DOXYGEN_OUTPUT_DIR}/main.css COPYONLY)
configure_file(${DOXYGEN_INPUT_DIR}/doxygen/footer.php ${DOXYGEN_OUTPUT_DIR}/footer.php COPYONLY)
configure_file(${DOXYGEN_INPUT_DIR}/doxygen/header.php ${DOXYGEN_OUTPUT_DIR}/header.php COPYONLY)
configure_file(${DOXYGEN_INPUT_DIR}/doxygen/footer.html ${DOXYGEN_OUTPUT_DIR}/footer.php COPYONLY)
configure_file(${DOXYGEN_INPUT_DIR}/doxygen/header.html ${DOXYGEN_OUTPUT_DIR}/header.php COPYONLY)

# target setup
add_custom_target(Doxygen-local ALL
                  COMMAND ${CMAKE_COMMAND} -E echo_append "Building Documentation..."
                  COMMAND ${DOXYGEN_EXECUTABLE} ${DOXYGEN_CONFIGURED_INPUT}
                  COMMAND ${CMAKE_COMMAND} -E echo "Done."
                  WORKING_DIRECTORY ${DOXYGEN_INPUT_DIR})

# configure the source LocalDoxyfile by copying it and replacing all @variables@
set(DOXYGEN_CONFIGURED_INPUT ${DOXYGEN_OUTPUT_DIR}/WebsiteDoxyfile)
configure_file(${DOXYGEN_INPUT_DIR}/doxygen/WebsiteDoxyfile ${DOXYGEN_CONFIGURED_INPUT} @ONLY)

# target setup
add_custom_target(Doxygen-website ALL
                  COMMAND ${CMAKE_COMMAND} -E echo_append "Building Documentation..."
                  COMMAND ${DOXYGEN_EXECUTABLE} ${DOXYGEN_CONFIGURED_INPUT}
                  COMMAND ${CMAKE_COMMAND} -E echo "Done."
                  WORKING_DIRECTORY ${DOXYGEN_INPUT_DIR})

# setup install rules
install(DIRECTORY ${DOXYGEN_OUTPUT_DIR}/LocalDocumentation
        DESTINATION ${INSTALL_MISC_DIR}
        COMPONENT doxygen)
