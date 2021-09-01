# Performance Analysis
The following tools are provided to display additional execution information.

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
