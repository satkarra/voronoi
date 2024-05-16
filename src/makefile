#================================================================#
#  VORONOI Makefile
# -------------------------------------------------------------- #
#
#  
#  Targets:
#    - voronoi : compile the VORONOI binary
#    - lglibs : compiles the LaGriT libraries used in VORONOI
#    - test : runs the test suite
#    - clean : destroys all build artifacts
#    - help : shows this help screen
#
#  Variables:
#    FC (default: gfortran) : Fortran MPI source compiler
#    FFLAGS : User-defined Fortran flags
#
#  Building:
#    To build VORONOI, you must first set four
#    environment variables:
#      - HDF5_DIR : /path/to/hdf5/
#      - LAGRIT_DIR : /path/to/LaGriT/
#      - PETSC_DIR : /path/to/petsc/
#      - PETSC_ARCH : dependant on sys. architecture
#
#    Further, `make lglibs` must be done before `make voronoi`.
#
#  Example:
#      $ export PETSC_DIR=/path/to/petsc 
#      $ export PETSC_ARCH=arch-darwin-c-opt
#      $ export HDF5_DIR=/path/to/hdf5/
#
#      $ make lglibs LAGRIT_DIR=../LaGriT/
#      $ make voronoi
#================================================================#

voronoi_src = ./
common_src   = ./

include ${PETSC_DIR}/lib/petsc/conf/variables
include ${PETSC_DIR}/lib/petsc/conf/rules

MYFLAGS = -I. -fcray-pointer -L${HDF5_DIR}/lib -I${HDF5_DIR}/include 

ifdef debug 
	MYFLAGS += ${FC_DEFINE_FLAG}DEBUG
endif

CFLAGS   =  
FFLAGS   = 
CPPFLAGS = ${MYFLAGS}
FPPFLAGS = ${MYFLAGS}

CLEANFILES       = voronoi 

# Begin Source Block
grid_obj = \
	${common_src}grid_aux.o\
	${common_src}grid.o\
	${common_src}voronoi_constants.o

# End Source Block
voronoi_obj = $(grid_obj) ${voronoi_src}voronoi.o

define VORONOI_HELP
----------------------- VORONOI MAKEFILE -----------------------

This is an automatic build tool for the VORONOI tessellation
software.

USAGE:

	make [options] [target]

TARGETS:

	- voronoi : compile the VORONOI binary
	- test : runs the test suite
	- clean : destroys all build artifacts
	- help : shows this help screen

VARIABLES:

	FC (default: gfortran) : Fortran MPI source compiler
	FFLAGS : User-defined Fortran flags
	HDF5_DIR : /path/to/hdf5/
	PETSC_DIR : /path/to/petsc/
	PETSC_ARCH : dependant on sys. architecture

BUILDING:

	To build VORONOI, you must first set four
	environment variables:
		- HDF5_DIR : /path/to/hdf5/
		- PETSC_DIR : /path/to/petsc/
		- PETSC_ARCH : dependant on sys. architecture

	then `make voronoi`.

EXAMPLE:

		> export PETSC_DIR=/path/to/petsc 
		> export PETSC_ARCH=arch-darwin-c-opt
		> export HDF5_DIR=/path/to/hdf5/

		> make voronoi

endef
export VORONOI_HELP

.PHONY: validate voronoi test help lglibs docs

voronoi :: validate $(voronoi_obj)
	${FLINKER} -o voronoi  $(voronoi_obj) \
	-L${HDF5_DIR}/lib -I${HDF5_DIR}/include \
	${PETSC_LIB} -lhdf5_fortran ${LIBS} 


validate :
	@CHECK=0
	@[ -z "${HDF5_DIR}" ] && echo "HDF5_DIR not defined" && exit 1 || CHECK=1
	@[ -z "${PETSC_DIR}" ] && echo "PETSC_DIR not defined" && exit 1 || CHECK=1
	@[ -z "${PETSC_ARCH}" ] && echo "PETSC_ARCH not defined" && exit 1 || CHECK=1
	@echo "All paths are set."

test : 
	cd ../test/sanity_check && python run_tests.py

clean :: 
	rm -f *.a,*.o,*.mod

%.mod : %.F90
	${FC} -c ${FC_FLAGS} ${FFLAGS} ${FCPPFLAGS} $<

help : 
	@echo "$$VORONOI_HELP"

# Dependencies stemming from "use" statements.
# These ensure that the module files are built in the correct order.
grid.o : voronoi_constants.o
voronoi.o : grid_aux.o grid.o 
