# Debugging

For debugging purposes NEC provides a number of helpful tools.

## Helpers

### NEC_TARGET_DELAY

To be able to attach a debugger to the target code more easily the `NEC_TARGET_DELAY` environment variable is provided.
When compiling an application with `NEC_TARGET_DELAY`, code is injected into the target executable,
which, at runtime, applies the value of this variable to the C sleep function,
as to delay the start of execution by that number of seconds.

!!! note
    If `NEC_TARGET_DELAY` is not set at runtime, then its value will default to zero.
