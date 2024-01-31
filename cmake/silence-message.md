# Silence messages

```cmake
function(message)
	if (NOT MESSAGE_QUIET)
		_message(${ARGN})
	endif()
endfunction()

set(MESSAGE_QUIET ON)
# Some command here
unset(MESSAGE_QUIET)
```

#cmake