![](docs/themes/kube/static/img/kube/voronoi_logo-black.png)

[![pipeline status](https://travis-ci.org/lanl/voronoi.svg?branch=master)](https://travis-ci.org/lanl/voronoi)

VORONOI is a parallel, scalable control volume tessellation generator, built for use in subsurface flow and transport solvers.

This fork is without integration with LaGriT and primarily for PFLOTRAN.

The program accepts a Delaunay mesh composed of one of four element types: triangles, tetrahedrals, quads, or hexes.

It then finds the Voronoi dual or median of that mesh, and writes it in a solver-specific format:

1. PFLOTRAN (`.uge`)
2. HDF5 (for general use; `.h5`)

### Features ###

* Accurate calculation of Voronoi/Median cell volume and cell face area in 2D and 3D
* Reads AVS input files
* Outputs to PFLOTRAN and HDF5
* Outputs visualization of control volume cells
* Built with PETSc for parallel execution and sparse matrix data types
* Cross-platform & open source

### Building ###

For building instructions, see the repo pages at https://github.com/satkarra/voronoi/blob/master/docs/content/docs/building.md



### Usage ###
 mpirun -np 4 ./voronoi -avs mesh_in_avs_fomrat.inp -type pflotran

### License ###

VORONOI is open-source software licensed under the 3-Clause BSD License. LANL Copyright No. C19012.

*This is open source software; you can redistribute it and/or modify it under
the terms of the BSD-3 License. If software is modified to produce derivative
works, such modified software should be clearly marked, so as not to confuse
it with the version available from LANL. Full text of the BSD-3 License can be
found in the LICENSE.md file of the repository.*

### Contact ###

Fork maintained by Satish Karra (karra@pnnl.gov).
To report a bug or feature request, open an issue on the GitHub Issue Tracker.

