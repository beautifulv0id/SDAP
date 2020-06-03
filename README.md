# Objective
Integrate the [SDPA software package](http://sdpa.sourceforge.net/download.html) in OpenGR to solve the SDP for the registration. [Here](https://sourceforge.net/projects/sdpa/files/sdpa/sdpa.7.1.1.manual.20080618.pdf/download) the link to the users manual. 

# Tasklist
- [x] export the SDP in matlab to sdpa file format
- [x] run and compare results using sdpa executable binary and cvx 
- [ ] generate the problem in C++ and use sdpa callable library to solve the problem (without using input file)

# Problem
Errors when trying to compile the `example1.cpp` in `/libexample` of the SDPA package. I put the make ouput into `make_logfile.txt`. 

# What I tried
It seems like I'm not linking to mumps correctly so so I added `/usr/lib/x86_64-linux-gnu/libdmumps.a` to `target_link_libraries` which is probably not the correct way! However, then I get an error like:

```
/usr/bin/ld: /usr/lib/x86_64-linux-gnu/libdmumps.a(dsol_bwd_aux.o): in function `dmumps_backslv_traiter_message_':
(.text+0xb16): undefined reference to `_gfortran_st_write'
/usr/bin/ld: (.text+0xb2b): undefined reference to `_gfortran_transfer_integer_write'
/usr/bin/ld: (.text+0xb3f): undefined reference to `_gfortran_transfer_character_write'
...
```
Which seems like I have to link to fortran too. Here I'm stuck a bit.. 

For reference, this is how they compile the examples using `g++`:
```
$ g++ -O3 -I$(HOME)/sdpa -I$(HOME)/lapack/include example1-1.cpp
$ g++ -O3 -o example1-1.exe example1-1.o -L$(HOME)/sdpa -lsdpa \
-L$(HOME)/lapack/lib -llapack -lcblaswr -lcblas -lf77blas -lI77 -lF77 -latlas
$ ./example1-1.exe example1.dat example1.out
```
> In the above command, we assume that we have installed ATLAS and LAPACK header file into
$(HOME)/lapack/include and library file into $(HOME)/lapack/lib, and SDPA into $(HOME)/sdpa.
