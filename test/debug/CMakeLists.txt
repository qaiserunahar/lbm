set_property(DIRECTORY PROPERTY LABELS debug)

add_executable(bad_alloc ${PROJECT_SOURCE_DIR}/app/debug/badalloc.f90)

add_executable(badbounds ${PROJECT_SOURCE_DIR}/app/debug/badbounds.f90)
target_compile_options(badbounds PRIVATE $<$<Fortran_COMPILER_ID:GNU>:-fcheck=bounds>)
