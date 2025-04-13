# Gadget4-install-manual

## 0. Gcc, CMake, git, gfortran 필요.

## 1. Install MPI & GSL & FFTW3 & HDF5 & HWLOC
```shell
sudo apt install mpich
sudo apt install libgsl-dev
sudo apt install libhdf5-dev
sudo apt install libfftw3-dev
sudo apt install libhwloc-dev hwloc
```

## 2. Download Gadget4
```shell
git clone http://gitlab.mpcdf.mpg.de/vrs/gadget4
```

## 3 IC files 추가
```shell
wget https://repository.prace-ri.eu/git/UEABS/ueabs/-/raw/r2.2-dev/gadget/example_ics.tar.gz
tar -xvf example_ics.tar.gz
```

## 4. Copy Template-Config.sh to Config.sh and Template-Makefile.systype to Makefile.systype

## 5. Makefile.systype 수정
```shell
#SYSTYPE=”hydra”
->
SYSTYPE=”hydra”
```

## 6. buildsystem/Makefile.path.hydra 수정
```shell
HDF5_INCL = -I/usr/include/hdf5/serial
HDF5_LIBS = -L/usr/lib/x86_64-linux-gnu/hdf5/serial
```

or find a exact directory.
```shell
find /usr -name hdf5.h
```
-> `/usr/include/path`
```shell
HDF5_INCL = -I/usr/include/path
```

```shell
find /usr -name libhdf5.so
```
-> `/usr/lib/path`
```shell
HDF5_LIBS = -I/usr/lib/path
```


## 7. make
```shell
$ make -j12
$ ./make-examples.sh
```

## 8.param.txt 수정 
```shell
/u/vrs/Simulations/ExampleICs/ics_collision_g4.dat.0
->
../../ExampleICs/ics_collision_g4.dat.0
```

## 9. Test run 돌리기 (examples/DM-L50-N128 경로로 가야됨. 20시간정도 소요.)
```shell
./Gadget4 param.txt
```

참고자료: https://kaizokuow.wordpress.com/2020/10/10/install-gadget4/
