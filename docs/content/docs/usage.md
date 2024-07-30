+++
title = "Usage"
description = "Command line usage for operating VORONOI"
date = 2018-10-22T12:17:12-06:00
weight = 20
draft = false
bref = "Command line usage for operating VORONOI"
toc = true
+++

### Command Line Usage ###

| Command                           | Functionality                               |
|-----------------------------------|---------------------------------------------|
| -avs [INFILE.inp]                 | AVS-UCD mesh to read                        |
| -type [pflotran,hdf5]             | filetype to write to                        |
| -cv [voronoi,median]              | control volume type                         |
| -d                                | write mesh statistics to stdout             |
| -o                                | filepath to save geometric coefficient data |

More detailed information can be run by calling

    voronoi -h

### Examples ###

**1. Converting a Delaunay AVS mesh to an PFLOTRAN sparse matrix**

As VORONOI has a native AVS reader, use the flag `-avs [file]` to input any AVS mesh.
Choose the file output type using the `-type [type]` flag. In this case, we are using FEHM.
Finally, the output filename can be chosen using the `-o [output]` argument.

    mpiexec -np 4 voronoi -avs my_mesh.inp -type pflotran -o my_mesh.uge



