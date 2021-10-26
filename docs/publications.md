# Publications

## Evaluating the Performance of OpenMP Offloading on the NEC SX-Aurora TSUBASA Vector Engine (2021)
???+ abstract
     The NEC SX-Aurora TSUBASA vector engine (VE) follows the tradition of long vector processors for high-performance computing (HPC). The technology combines the vector computing capabilities with the popularity of standard x86 architecture by integrating it as an accelerator. To decrease the burden of code porting for different accelerator types, the OpenMP specification is designed to be single parallel programming model for all of them. Besides the availability of compiler and runtime implementations, the functionality as well as the performance is important for the usability and acceptance of this paradigm. In this work, we present LLVM-based solutions for OpenMP target device offloading from the host to the vector engine and vice versa (reverse offloading). Therefore, we use our source-to-source transformation tool sotoc as well as the native LLVM-VE code path. We assess the functionality and present the first performance numbers of real-world HPC kernels. We discuss the advantages and disadvantage of the different approaches and show that our implementation is competitive to other GPU OpenMP runtime implementations. Our work gives scientific programmers new opportunities and flexibilities for the development of scalable OpenMP offloading applications for SX-Aurora TSUBASA.

??? cite
    ``` text
    Cramer, T., Kosmynin, B., Moll, S., Römmer, M., Focht, E., & Müller, M. (2021). Evaluating the Performance of OpenMP Offloading on the NEC SX-Aurora TSUBASA Vector Engine. Supercomputing Frontiers And Innovations, 8(2), 59-74. doi:http://dx.doi.org/10.14529/jsfi210204
    ```

??? cite "BibTeX"
    {% raw %}
    ``` bibtex
    @article{ref:Cramer2021,
    title = {{E}valuating the {P}erformance of {O}pen{MP} {O}ffloading on the {NEC} {SX}-{A}urora {TSUBASA} {V}ector {E}ngine},
    author = {Tim Cramer and Boris Kosmynin and Simon Moll and Manoel Römmer and Erich Focht and Matthias Müller},
    journal = {Supercomputing Frontiers and Innovations},
    volume = {8},
    number = {2},
    year = {2021},
    keywords = {HPC, OpenMP, offloading, reverse offloading, vector computing, performance},
    abstract = {The NEC SX-Aurora TSUBASA vector engine (VE) follows the tradition of long vector processors for high-performance computing (HPC). The technology combines the vector computing capabilities with the popularity of standard x86 architecture by integrating it as an accelerator. To decrease the burden of code porting for different accelerator types, the OpenMP specification is designed to be single parallel programming model for all of them. Besides the availability of compiler and runtime implementations, the functionality as well as the performance is important for the usability and acceptance of this paradigm. In this work, we present LLVM-based solutions for OpenMP target device offloading from the host to the vector engine and vice versa (reverse offloading). Therefore, we use our source-to-source transformation tool sotoc as well as the native LLVM-VE code path. We assess the functionality and present the first performance numbers of real-world HPC kernels. We discuss the advantages and disadvantage of the different approaches and show that our implementation is competitive to other GPU OpenMP runtime implementations. Our work gives scientific programmers new opportunities and flexibilities for the development of scalable OpenMP offloading applications for SX-Aurora TSUBASA.},
    issn = {2313-8734},
    url = {https://superfri.org/superfri/article/view/385}
    }
    ```
    {% endraw %}
## OpenMP Target Device Offloading for the SX-Aurora TSUBASA Vector Engine (2020)
???+ abstract
     Driven by the heterogeneity trend in modern supercomputers, OpenMP provides support for heterogeneous systems since 2013. Having a single programming model for all kinds of accelerator-based systems decreases the burden of code porting to different device types. The acceptance of this heterogeneous paradigm requires the availability of corresponding OpenMP compiler and runtime environments supporting different target device architectures. The LLVM/Clang infrastructure is designated to extend the offloading features for any new target platform. However, this supposes a compatible compiler backend for the target architecture. In order to overcome this limitation we present a source-to-source code transformation technique which outlines the OpenMP code regions for the target device. By combining this technique with a corresponding communication layer, we enable OpenMP target offloading to the NEC SX-Aurora TSUBASA vector engine, which represents the new generation of vector computing.

??? cite
    ``` text
    Cramer T., Römmer M., Kosmynin B., Focht E., Müller M.S. (2020) OpenMP Target Device Offloading for the SX-Aurora TSUBASA Vector Engine. In: Wyrzykowski R., Deelman E., Dongarra J., Karczewski K. (eds) Parallel Processing and Applied Mathematics. PPAM 2019. Lecture Notes in Computer Science, vol 12043. Springer, Cham. https://doi.org/10.1007/978-3-030-43229-4_21
    ```

??? cite "BibTeX"
    {% raw %}
    ``` bibtex
    @inproceedings{ref:Cramer2020,
    title        = {{O}pen{MP} {T}arget {D}evice {O}ffloading for the {SX}-{A}urora {TSUBASA} {V}ector {E}ngine},
    author       = {Cramer, Tim and Römmer, Manoel and Kosmynin, Boris and Focht, Erich and Müller, Matthias S.},
    year         = 2020,
    booktitle    = {Parallel Processing and Applied Mathematics : 13th International Conference, PPAM 2019, Bialystok, Poland, September 8-11, 2019, Revised Selected Papers, edited by Roman Wyrzykowski, Ewa Deelman, Jack Dongarra, Konrad Karczewski},
    publisher    = {Springer International Publishing [2020.] ; Cham : Imprint:	Springer [2020.]},
    address      = {Cham},
    series       = {Theoretical Computer Science and General Issues},
    volume       = 12043,
    pages        = {237--249},
    reportid     = {RWTH-2020-04830},
    comment      = {Parallel Processing and Applied Mathematics : 13th International Conference, PPAM 2019, Bialystok, Poland, September 8-11, 2019, Revised Selected Papers, Part I / edited by Roman Wyrzykowski, Ewa Deelman, Jack Dongarra, Konrad Karczewski},
    organization = {13th International Conference on Parallel Processing and Applied Mathematics}
    }
    ```
    {% endraw %}

--8<-- "includes/abbreviations.md"
