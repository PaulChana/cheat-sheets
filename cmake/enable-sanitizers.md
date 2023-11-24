# Enable sanitizers

```cmake
option (ENABLE_SANITIZERS "Whether to enable sanitizers" OFF)

function (enable_sanitizer target type)
    if (CMAKE_CXX_COMPILER_ID MATCHES "MSVC")
        message (DEBUG "Enabling sanitizer: ${type}")
        target_compile_options (${target} PRIVATE "/fsanitize=${type}")
    endif ()
    if (CMAKE_CXX_COMPILER_ID MATCHES "Clang")
        message (DEBUG "Enabling sanitizer: ${type}")
        target_compile_options (${target} PRIVATE "-fsanitize=${type}")
        target_link_options (${target} PRIVATE "-fsanitize=${type}")
    endif ()
endfunction (enable_sanitizer)

function (enable_sanitizers target)
    if (NOT ENABLE_SANITIZERS)
        return
    endif()

    if (NOT SANITIZE_ADDRESS AND NOT SANITIZE_THREAD AND NOT SANITIZE_UNDEFINED)
        message (FATAL_ERROR
                "[Sanitizers]: No sanitizer has been enabled. Define one of SANITIZE_ADDRESS, SANITIZE_THREAD, SANITIZE_UNDEFINED")
        return
    endif ()

    if (SANITIZE_ADDRESS)
        message (STATUS "[Sanitizers]: ASAN enabled for ${target}")
        enable_sanitizer (${target} address)
    endif ()

    if (SANITIZE_THREAD)
        message (STATUS "[Sanitizers]: TSAN enabled for ${target}")
        enable_sanitizer (${target} thread)
    endif ()

    if (SANITIZE_UNDEFINED)
        message (STATUS "[Sanitizers]: UBSAN enabled for ${target}")
        enable_sanitizer (${target} undefined)
    endif ()
endfunction (enable_sanitizers)

```

#cmake