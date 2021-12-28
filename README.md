# WRF_install
安装 WRF 脚本
## 命令
```shell
sudo apt update
sudo apt upgrade
sudo apt autoremove
sudo apt install build-essential gfortran csh libpng-dev cmake


cd /opt && mkdir WRF && cd WRF && mkdir Downloads && mkdir Library
cd Downloads
wget https://file-1258430491.cos.ap-shanghai.myqcloud.com/hdf5-1.13.0.tar.gz
tar -xvzf hdf5-1.10.5.tar
cd hdf5-1.13.0/
./configure --prefix=/opt/WRF/Library --with-zlib --enable-hl --enable-fortran
make check -j
make install

export HDF5=/opt/WRF/Library
export LD_LIBRARY_PATH=/opt/WRF/Library/lib:$LD_LIBRARY_PATH

cd ..
wget https://downloads.unidata.ucar.edu/netcdf-c/4.8.1/src/netcdf-c-4.8.1.tar.gz
tar -xvzf netcdf-c-4.8.1.tar.gz 
cd netcdf-c-4.8.1
export CPPFLAGS=-I/opt/WRF/Library/include 
export LDFLAGS=-L/opt/WRF/Library/lib
./configure --prefix=/opt/WRF/Library --disable-dap
make check -j
make install

export PATH=/opt/WRF/Library/bin:$PATH
export NETCDF=/opt/WRF/Library/


cd ..
wget https://downloads.unidata.ucar.edu/netcdf-fortran/4.5.3/netcdf-fortran-4.5.3.tar.gz
tar -xvzf netcdf-fortran-4.5.3.tar.gz
cd netcdf-fortran-4.5.3
export LIBS="-lnetcdf -lhdf5_hl -lhdf5 -lz" 
./configure --prefix=/opt/WRF/Library/ --disable-shared
make check -j
make install

cd ..
wget https://ece.engr.uvic.ca/~frodo/jasper/software/jasper-2.0.14.tar.gz
tar -xvzf jasper-2.0.14.tar.gz
cmake -G "Unix Makefiles" -H . -B./build -DCMAKE_INSTALL_PREFIX=/opt/WRF/Library/
cd build
make -j
make install 
export JASPERLIB=/opt/WRF/Library/lib
export JASPERINC=/opt/WRF/Library/include


cd ..
wget https://github.com/wrf-model/WRF/archive/refs/tags/v4.3.2.tar.gz
tar -xvzf v4.3.2.tar.gz -C ../
cd ../WRF-4.3.2/
./clean
sh -c '/bin/echo -e "33" echo -e "1" |sh ./configure'
./compile em_real
export WRF_DIR=/opt/WRF/WRF-4.1.2


cd ..
wget https://github.com/wrf-model/WPS/archive/v4.3.1.tar.gz
tar -xvzf v4.3.1.tar.gz
cd WPS-4.3.1
./comfigure
./compile
```