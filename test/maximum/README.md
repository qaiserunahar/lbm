# Maximum name lengths

Fortran 2003 specifies maximum name length of 63 for syntax elements like modules, submodules, procedures, variables, etc.

These are a few configure-time checks that the compiler supports these.
For example, GCC 10 and Intel oneAPI pass all these checks.

Maximum line length of free-form (modern) Fortran source is officially 132 character, but compilers such as Intel oneAPI allow lines thousands of characters long by default.
