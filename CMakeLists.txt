cmake_minimum_required(VERSION 3.14)

function(dump_cmake_variables)
    get_cmake_property(_variableNames VARIABLES)
    list (SORT _variableNames)
    foreach (_variableName ${_variableNames})
        if (ARGV0)
            unset(MATCHED)
            string(REGEX MATCH ${ARGV0} MATCHED ${_variableName})
            if (NOT MATCHED)
                continue()
            endif()
        endif()
        message(STATUS "${_variableName}=${${_variableName}}")
    endforeach()
endfunction()

# set(CXX_STANDARD 17)

# project(gtkmm_example)

# find_package(GTK 3.0 REQUIRED)

# dump_cmake_variables(GTK)


# include_directories("${GTK2_INCLUDE_DIRS}")

# # aux_source_directory("${CMAKE_SOURCE_DIR}/src" MYSOURCES)

# # # "${GTK2_GDKMM_INCLUDE_DIR}"



# add_executable("${CMAKE_PROJECT_NAME}" main.cpp "${MYSOURCES}")

# target_link_libraries("${CMAKE_PROJECT_NAME}" "${GTK2_LIBRARIES}")

set(CXX_STANDARD 99)

project(example)

find_package(PkgConfig)

pkg_check_modules(GTKMM gtkmm) # look into FindPkgConfig.cmake, 
                                                                # it contains documentation
# Now the variables GTKMM_INCLUDE_DIRS, GTKMM_LIBRARY_DIRS and GTKMM_LIBRARIES 
# contain what you expect 

# add_subdirectory(src) 

dump_cmake_variables(GTKMM)

link_directories(${GTKMM_LIBRARY_DIRS})

include_directories(${GTKMM_INCLUDE_DIRS})

add_executable(example main.cpp)

target_link_libraries(example ${GTKMM_LIBRARIES})