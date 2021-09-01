# Debugging

For debugging purposes NEC provides a number of helpful tools.

## Libomptarget
If the debug-version of libomptarget was build, `LIBOMPTARGET_DEBUG=1` can be used to show additional debugging information at runtime.

!!! tip
    Use `LIBOMPTARGET_DEBUG=4` to dump host-target pointer mappings.

## log4crc
See [Debugging with log4crc](https://sx-aurora.github.io/posts/Debugging-with-log4crc/){target=_blank} by Erich Focht

## `PROGINF`
`PROGINF` provides program execution analysis information throughout the execution of program.
To use `PROGINF` compile your C code using `ncc`. The `PROGINF`-library is linked by default.
When setting `VE_PROGINF` to `YES` or `DETAIL` at runtime, additional information will be displayed.
For additional information see the [`PROGINF` and `FTRACE` users guide](https://www.hpc.nec/documents/sdk/pdfs/g2at03e-PROGINF_FTRACE_User_Guide_en.pdf){target=_blank}.

## `FTRACE`
`FTRACE` is used to obtain performance information such as the CPU usage and vectorization
aspect of each function in a program, as well as user regions.
To use `FTRACE` compile your C code using `ncc` with the `-ftrace` flag.
When executing, a `ftrace.out.*` file is generated, which can be viewed using `#!shell ftrace -f ftrace.out.*`.
For additional information see the [`PROGINF` and `FTRACE` users guide](https://www.hpc.nec/documents/sdk/pdfs/g2at03e-PROGINF_FTRACE_User_Guide_en.pdf){target=_blank}
and the [NEC `FTRACE` Viewer users guide](https://www.hpc.nec/documents/sdk/pdfs/g2at01e-NEC_Ftrace_Viewer_User_Guide_en.pdf){target=_blank}.

## NEC Parallel Debugger
The NEC parallel debugger can be invoked from within the eclipse IDE.
For detailed instructions see the [users guide](https://www.hpc.nec/documents/sdk/pdfs/g2at02e-NEC_ParallelDebugger_UsersGuide.pdf){target=_blank}.

## GDB
NEC provides a ported version of `gdb` for VE with specific commands and abilities for them.
There are the following difference points between the ported version of GDB for VE and GDB for Linux:

1. GDB internally executes `ve_exec` command with `--traceme` option in order to execute VE program.

2. VE_NODE_NUMBER environment variable can be used to specify VE node to execute VE program.
   If the environment variable is not set, VE program is executed on VE node 0.

3. Only local debugging is supported. Remote debugging using GDB server or GDB stub is not supported.

4. The directory where separate debug symbols are searched for is `/opt/nec/ve/lib/debug`.

5. GDB can not deal with thread-local variables correctly, because DWARF information about them is invalid.

6. The following commands don't show information for VE side but show for VH(Vector Host) side using procfs of it.
   ```
    info proc
    info proc all
    info proc cmdline
    info proc cwd
    info proc exe
    info proc mappings
    info proc stat
    info proc status
    ```

7. `info auxv` command is available only in debugging with core file.

8. GDB and VEOS does not handle invocation of `execve()` system call from a VE program properly.
   When a VE program invokes `execve()` system call, GDB detects `SIGTRAP`, or can not find the process or the thread,
   and then it does not reload a new program.
   In this case, `quit` command need to be executed to terminate GDB.
   The debugged process will be killed when GDB terminates, if it has been executed from GDB.

9. `call` command can be used to invoke a function of a VE program. But, if stack area beyond page boundary
   is required, `call` command fails due to access error.

12. Instruction Counter (IC) will be far from the address which causes a HW exception when the program is
    stopped by the HW exception.
    `advance off` mode can be set in order to check the precise state when HW exception occurs.
    In this mode, instruction execution is held until the preceding instructions have completed.
    As the result, GDB shows the precise state when HW exception occurs.

A full list of differences con be found [here](https://www.hpc.nec/documents/veos/en/gdb/Difference_Points_GDB.htm){target=_blank}.

## Helpers
### Delay Target Code Execution
To be able to attach a debugger to the target code more easily the `NEC_TARGET_DELAY` environment variable is provided.
When compiling an application with `NEC_TARGET_DELAY`, code is injected into the target executable,
which, at runtime, applies the value of this variable to the C sleep function,
as to delay the start of execution by that number of seconds.

!!! note
    If `NEC_TARGET_DELAY` is not set at runtime, then its value will default to zero.

--8<-- "includes/abbreviations.md"
