# Publications

## OpenMP Target Device Offloading for the SX-Aurora TSUBASA Vector Engine
!!! abstract
    Driven by the heterogeneity trend in modern supercomputers, OpenMP provides support for heterogeneous systems since 2013. Having a single programming model for all kinds of accelerator-based systems decreases the burden of code porting to different device types. The acceptance of this heterogeneous paradigm requires the availability of corresponding OpenMP compiler and runtime environments supporting different target device architectures. The LLVM/Clang infrastructure is designated to extend the offloading features for any new target platform. However, this supposes a compatible compiler backend for the target architecture. In order to overcome this limitation we present a source-to-source code transformation technique which outlines the OpenMP code regions for the target device. By combining this technique with a corresponding communication layer, we enable OpenMP target offloading to the NEC SX-Aurora TSUBASA vector engine, which represents the new generation of vector computing.

??? cite
    Cramer T., Römmer M., Kosmynin B., Focht E., Müller M.S. (2020) OpenMP Target Device Offloading for the SX-Aurora TSUBASA Vector Engine. In: Wyrzykowski R., Deelman E., Dongarra J., Karczewski K. (eds) Parallel Processing and Applied Mathematics. PPAM 2019. Lecture Notes in Computer Science, vol 12043. Springer, Cham. https://doi.org/10.1007/978-3-030-43229-4_21

--8<-- "includes/abbreviations.md"
