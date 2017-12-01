# README
This respository contains the files and instructions you need to modify MOOG in order to reproduce the spectral synthesis calculations in Carlberg et al. (2018).  The full MOOG code can be obtained from Chris Sneden's [MOOG website](http://www.as.utexas.edu/~chris/moog.html). The modifications have been made to the 2014 source code.

## Instructions for modifying MOOG
Three of the existing MOOG subroutines must be replaced with the versions in this repository. They are:
1. **Atmos.com** - increased the dimensions of 'numdems' variable increased numdens's dimensions
2. **Inmodel.f** - include CH/NH in the numdens variable, also fixed definition of numdens for elements NOT controlled by molecular equilibrium (true when molset=0)
3. **Kappa.com**  - adds the new opacity variablestoin the global variable domain
4. **Opacit.f** - calls the new CH/NH opacity calculation subroutine and adds results to total opacity. Prints out the new opacities to stdout (atmosphere = 2 in driver file)

The new edits should be marked with with my initials (JKC) in the source code. 

One new code (Opacmoled.f) must be added to the list of compiled files. This code contains the tables of molecular dissociation opacities for CH and NH and will calculate the appropriate opacity for a given atmosphere layer by interpolating the values in the table.

To recompile MOOG with the new changes, the following steps are required in the Makefile that you are using:
1. add Opacmoled.o to the list of OBJECTS
2. in the compilation line, change the name of the compiled module to avoid overwriting your regular MOOG code. E.g., "-o MOOG_mod"

## Input files for running MOOG.
1. be_line_list.txt - the MOOG formatted line list for generating spectra near 3130 angstroms
2. dummy_driver.txt - an example driver file needed to run MOOG


