find_package(OpenMP COMPONENTS Fortran)

include(CheckFortranSourceCompiles)
set(CMAKE_REQUIRED_FLAGS ${OpenMP_Fortran_FLAGS})
set(CMAKE_REQUIRED_INCLUDES ${OpenMP_Fortran_INCLUDE_DIRS})
set(CMAKE_REQUIRED_LIBRARIES ${OpenMP_Fortran_LIBRARIES})

if(OpenMP_Fortran_FOUND)

check_fortran_source_compiles(
"program test
use, intrinsic:: iso_fortran_env, only: int64
implicit none
integer(int64), external :: omp_get_wtick
integer(int64) :: rate
rate = omp_get_wtick()
end program"
HAS_OpenMP
SRC_EXT f90
)

endif()

if(NOT HAS_OpenMP)
  message(STATUS "OpenMP tests skipped")
  return()
endif()

set_property(DIRECTORY PROPERTY LABELS openmp)


add_executable(timeprec ${PROJECT_SOURCE_DIR}/src/openmp/timeprec.f90)
target_link_libraries(timeprec PRIVATE OpenMP::OpenMP_Fortran)
add_test(NAME TimeMeasure COMMAND timeprec)
set_property(TEST TimeMeasure PROPERTY RUN_SERIAL true)

add_executable(jacobi jacobi_openmp.f90)
target_link_libraries(jacobi PRIVATE OpenMP::OpenMP_Fortran)
add_test(NAME Jacobi COMMAND jacobi)
set_property(TEST Jacobi PROPERTY RUN_SERIAL true)
