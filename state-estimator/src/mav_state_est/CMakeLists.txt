file(GLOB hpp_files *.hpp)

# make the headers public
pods_install_headers(${hpp_files} DESTINATION mav_state_est)


file(GLOB cpp_files *.cpp)

# make a state estimator library 
add_library(mav-state-est SHARED ${cpp_files})

set(REQUIRED_LIBS bot2-core
	bot2-param-client
	bot2-frames
	eigen-utils
        lcmtypes_pronto
#    lcmtypes_microstrain
#    lcmtypes_${POD_NAME}
#    lcmtypes_mav-lcmtypes
    )
pods_use_pkg_config_packages(mav-state-est ${REQUIRED_LIBS})
pods_install_libraries(mav-state-est)
pods_install_pkg_config_file(mav-state-est
    CFLAGS
    LIBS -lmav-state-est
    REQUIRES 	${REQUIRED_LIBS}
    VERSION 0.0.1)
