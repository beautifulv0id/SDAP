# Objective
Integrate the [SDPA software package](http://sdpa.sourceforge.net/download.html) in OpenGR to solve the SDP for the registration. [Here](https://sourceforge.net/projects/sdpa/files/sdpa/sdpa.7.1.1.manual.20080618.pdf/download) the link to the users manual.

# Compilation instruction
Install required packages:
```bash
sudo apt-get install gfortran
```

Download and compile SDPA:
```bash
cd SDPA
mkdir external && cd external
wget https://sourceforge.net/projects/sdpa/files/sdpa/sdpa_7.3.8.tar.gz
tar -xvzf sdpa_7.3.8.tar.gz sdpa-7.3.8/
cd sdpa-7.3.8/
./configure --prefix=$PWD/.. 
make && make install
cd ..
git clone https://github.com/xianyi/OpenBLAS.git
cd OpenBLAS
make BINARY=64 CC=gcc FC=gfortran USE_OPENMP=0 NO_CBLAS=1 NO_WARMUP=1 libs netlib
cd ../..
mkdir build && cd build
cmake .. -DSDPA_ROOT_DIR=../external/
```
