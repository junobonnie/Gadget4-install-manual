# Gadget4-install-manual

0. Gcc, CMake, git, gfortran 필요.

1. Install MPI
$ sudo tar xvfz mpich-4.1.1.tar.gz
$ cd mpich-4.1.1
$ sudo ./configure -prefix=/opt/mpich/4.1.1
$ sudo make
$ sudo make install

2. Install gsl
$ sudo tar xvfz gsl-2.5.tar.gz
$ cd gsl-2.5
$ sudo ./configure -prefix=/opt/gsl/2.5
$ sudo make
$ sudo make install

3. Install FFTW3
$ sudo tar xvfz fftw-3.3.8.tar.gz
$ cd fftw-3.3.8
$ sudo ./configure -prefix=/opt/fftw/3.3.8 -enable-openmp
$ sudo make
$ sudo make install

4. Install hdf5
$ sudo tar xvfz hdf5-1.10.1.tar.gz
$ cd hdf5-1.10.1
$ sudo ./configure -prefix=/opt/hdf5/1.10.1
$ sudo make
$ sudo make install

5. Install hwloc
$ sudo tar xvfz hwloc-2.2.0.tar.gz
$ cd hwloc-2.2.0
$ sudo ./configure -prefix=/opt/hwloc/2.2.0
$ sudo make
$ sudo make install

6. .bashrc 수정
export GSL_HOME=${HOME}/lib/gsl/2.5
export FFTW3_HOME=${HOME}/lib/fftw/3.3.8
export HDF5_HOME=${HOME}/lib/hdf5/1.10.1
export MPICH_HOME=${HOME}/lib/mpich/4.1.1
export HWLOC_HOME=${HOME}/lib/hwloc/2.2.0
export LD_LIBRARY_PATH=${GSL_HOME}/lib:${FFTW3_HOME}/lib:${HDF5_HOME}/lib:${MPICH_HOME}/lib:${HWLOC_HOME}/lib:$LD_LIBRARY_PATH
export PATH=${GSL_HOME}/bin:${FFTW3_HOME}/bin:${HDF5_HOME}/bin:${MPICH_HOME}/bin:${HWLOC_HOME}/bin:$PATH

6.5 경로변수 확인
$ source .bashrc
$ echo ${GSL_HOME}
$ echo ${FFTW3_HOME}
$ echo ${HDF5_HOME}
$ echo ${MPICH_HOME}
$ echo ${HWLOC_HOME}
$ echo ${LD_LIBRARY_PATH}
$ echo ${PATH}

7. Download Gadget4
git clone http://gitlab.mpcdf.mpg.de/vrs/gadget4

7.5 IC files 추가
tar -xvf example_ics.tar

param.txt 수정 ../../ICs/ExampleICs/
/u/vrs/Simulations/ICs/ExampleICs/ics_collision_g4.dat.0

8. Copy Template-Config.sh to Config.sh and Template-Makefile.systype to Makefile.systype

9. Makefile.systype 수정
#SYSTYPE=”hydra”
->
SYSTYPE=”hydra”

10. buildsystem/Makefile.path.hydra 수정
GSL_INCL = -I${GSL_HOME}/include
GSL_LIBS = -L${GSL_HOME}/lib
FFTW_INCL = -I${FFTW3_HOME}/include
FFTW_LIBS = -L${FFTW3_HOME}/lib
HDF5_INCL = -I${HDF5_HOME}/include
HDF5_LIBS = -L${HDF5_HOME}/lib
HWLOC_INCL = -I${HWLOC_HOME}/include
HWLOC_LIBS = -L${HWLOC_HOME}/lib

11. make -j12

12. bash Make-examples.sh
* cannot find -lfftw3f 오류 발생시, $ sudo apt install fftw3-dev

13. Test run 돌리기 (examples/DM-L50-N128 경로로 가야됨. 20시간정도 소요.)
./Gadget4 param.txt


참고자료: https://kaizokuow.wordpress.com/2020/10/10/install-gadget4/
