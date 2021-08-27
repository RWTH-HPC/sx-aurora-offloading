# Installation
!!! danger "Attention"
    This page is for internal and development use only.

## Installation Script
``` shell
#!/bin/bash
set -e

module purge
module load DEVELOP cmake clang

FILE_SYS="/scratch/${USER}"

BUILD_DIR="${FILE_SYS}/clang-dev/BUILD"
SRC_DIR="${HOME}/llvm-project/llvm"
INSTALL_DIR="${HOME}/install/clang-dev/install"

echo "Building in $BUILD_DIR"
mkdir -p "${BUILD_DIR}"

(cd "${BUILD_DIR}"

cmake -DCMAKE_C_COMPILER=clang \
    -DCMAKE_CXX_COMPILER=clang++ \
    -DLLVM_ENABLE_PROJECTS="clang;openmp;libcxx;libcxxabi" \
    -DCMAKE_BUILD_TYPE=Debug \
    -DBUILD_SHARED_LIBS=ON \
    -DCMAKE_INSTALL_PREFIX="${INSTALL_DIR}" \
    -DLLVM_INSTALL_UTILS=OFF \
    -DLIBOMP_TSAN_SUPPORT=OFF \
    -DLLVM_TOOL_LLDB_BUILD=OFF \
    -DLLVM_BUILD_DOCS=OFF \
    -DOPENMP_ENABLE_LIBOMPTARGET=ON \
    -DNECAURORA_TARGET_COMPILER=/opt/nec/ve/ncc/3.0.8/bin/ncc \
    -DSOTOC_ENABLE_TESTS=ON \
    "${SRC_DIR}" || exit 21
    nice make -j 31 install || exit 42)
```

## Module File
!!! NOTE
    Don't forget to set `$MODULEPATH`

``` shell
#%Module1.0#####################################################################
###
### clang-dev
###
set MAJORVERSION "13"
set MINORVERSION "0"
set REVISION     "0"

set VERSION "13.0.0"

set BASE "${HOME}/install/clang-dev/install"
set AVEO "${HOME}/aveo/install"

set module_base_path /usr/local_rwth/modules/modulefiles/source

source "$module_base_path/FUNCTIONS/output"
source "$module_base_path/FUNCTIONS/module_management"
source "$module_base_path/FUNCTIONS/compiler_env"
source "$module_base_path/FUNCTIONS/usage_log"

log_module_load clang-dev/$VERSION

proc ModulesHelp { } {
	global VERSION
	puts stderr "This module initializes the llvm environment including clang and libomp"
	puts stderr "See \thttps://github.com/llvm-mirror/"
}

module-whatis	"initialize clang-dev ($VERSION)"

# machine specific names/directories
set runTimeLinker ""
if ![info exists HOST] {
	switch [uname machine] {
		i686 {
			set HOST "i686-pc-linux-gnu"
			set runTimeLinker "-Wl,-rpath="
		}
		x86_64 {
			set HOST "x86_64-unknown-linux-gnu"
			set EXTRALIB "lib64"
			set runTimeLinker "-Wl,-rpath="
		}
	}
}
set CLANG "$BASE"

# if module should be loaded, check for conflicts and print info
switch [module-info mode] {
	load {
		# is this module already loaded?
		set conflict clang-dev/$VERSION
		if { [is-loaded $conflict]} { # print a yellow waring at the end of the line
			m_warning "$conflict already loaded, doing nothing"
			exit
		}
		# define conflicts here (example the conflicting module)
		set conflict clang
		if { [is-loaded $conflict]} { #print a red error at the end of the line
			m_error "$conflict already loaded and conflicts with clang.\nTry unloading $conflict first"
			break
		}
		# check if software is really installed, if not error
		if { ![file isdirectory $CLANG/bin] } {
			m_error "This software is not installed on this machine. Please try anotherone"
			break
		}
		# if no conflicts are found print string and a green ok at the end of the line
		m_success "Loading clang-dev $VERSION"
    }
    unload {
		m_success "Unloading clang-dev $VERSION"
	}
}

prepend-path PATH            $CLANG/bin
prepend-path MANPATH         $CLANG/share/man
prepend-path LD_LIBRARY_PATH $CLANG/lib
prepend-path LD_LIBRARY_PATH $AVEO/lib
prepend-path LIBRARY_PATH    $CLANG/lib
set          linkflags    "-L$CLANG/lib "

set RUNPATH  "$rpathreplacestring$CLANG/lib"
set GCCRPATH ""

setenv LLVM_ROOT                $CLANG
setenv CLANG_ROOT               $CLANG
prepend-path C_INCLUDE_PATH     $CLANG/include
prepend-path CPLUS_INCLUDE_PATH $CLANG/include
prepend-path CPATH              $CLANG/include
prepend-path CPATH              $CLANG/lib/clang/$VERSION/include

init_compiler "clang" $MAJORVERSION $MINORVERSION $REVISION

set_compiler "CLANG_" 	FC 			" "
set_compiler "CLANG_" 	F77 			" "
set_compiler "CLANG_" 	CC 			clang
set_compiler "CLANG_" 	CXX 			clang++
set_compiler "CLANG_" 	OBJC 			clang
set_compiler "CLANG_" 	OBJCXX 			clang++

set_compiler_flags "CLANG_" "DEBUG"		"-g"
set_compiler_flags "CLANG_" "FAST" 		"-O3 -ffast-math -mtune=native"
set_compiler_flags "CLANG_" "FAST_NO_FPOPT" 	"-O3 -mtune=native"
set_compiler_flags "CLANG_" "AUTOPAR"		" "
set_compiler_flags "CLANG_" "OPENMP"		" -fopenmp "

set_compiler_flags "CLANG_" "ARCH32"		" -m32 "
set_compiler_flags "CLANG_" "ARCH64"		" -m64 "
set_compiler_flags "CLANG_" "FREE"		" -ffree-form "
set_compiler_flags "CLANG_" "LINKER" 		" $linkflags "
set_compiler_flags "CLANG_" "PIC" 		"-fPIC -DPIC -shared"

#needed for MPI and lapacks
set_compiler_flags "CLANG_" "RUNTIME_LINKER" "$runTimeLinker"

#FLAGS_L|RPATH shared beween all modules
prependable_variable_list "FLAGS_LPATH" " $linkflags " "clang"
prependable_variable_list_withreplace "FLAGS_RPATH" "$RUNPATH $GCCRPATH" "clang" $rpathreplacestring $runTimeLinker
```

--8<-- "includes/abbreviations.md"
