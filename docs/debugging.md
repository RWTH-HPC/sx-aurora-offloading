# Debugging

For debugging purposes NEC provides a number of helpful tools.

## Libomptarget
If the debug-version of libomptarget was build, `LIBOMPTARGET_DEBUG=1` can be used to show additional debugging information at runtime.

!!! tip
    Use `LIBOMPTARGET_DEBUG=4` to dump host-target pointer mappings.

## log4crc
See [Debugging with log4crc](https://sx-aurora.github.io/posts/Debugging-with-log4crc/) by Erich Focht

## Helpers
### NEC_TARGET_DELAY
To be able to attach a debugger to the target code more easily the `NEC_TARGET_DELAY` environment variable is provided.
When compiling an application with `NEC_TARGET_DELAY`, code is injected into the target executable,
which, at runtime, applies the value of this variable to the C sleep function,
as to delay the start of execution by that number of seconds.

!!! note
    If `NEC_TARGET_DELAY` is not set at runtime, then its value will default to zero.

--8<-- "includes/abbreviations.md"
