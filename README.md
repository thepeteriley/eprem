# EPREM

A simplified, open-source version of the Energetic Particle Radiation Environment Module

## Installation

First, clone the repository
```
git clone https://github.com/myoung-space-science/eprem.git
```

The simplest way to configure, build, and install EPREM is by running `setup.sh`. Type `./setup.sh --help` to learn about its options.

To configure and build EPREM, then install the executable in your home directory, run
```
./setup.sh --install -- --prefix=$HOME
```
Note that the `--` before `--prefix` is necessary to tell `setup.sh` that you wish to pass the `--prefix` argument to `configure.sh`. In fact, this is true of any argument that `configure.sh` accepts (see `./configure --help`).

Although `setup.sh` intends to get you up and running as quickly as possible, you will likely need to specify some configuration options. In particular, you will need to point `configure.sh` to installations of [libconfig](http://hyperrealm.github.io/libconfig/) and [NetCDF4](https://unidata.github.io/netcdf4-python/) if they are not already in your `$PATH`. To do so, provide the `--with-libconfig-dir=...` and `--with-netcdf-dir=...` arguments. In the less likely event that there is no MPI distribution in your `$PATH`, you will need to provide the `--with-mpi-dir=...` argument. 

If your system is 'vanilla' (e.g., a new installation) and doesn't have support for autoconf, MPI, libconfig, or netCDF, you'll need to add them. For Debian-based systems (tested with 22.04 Ubuntu), you can run the following commands:

```
$ sudo apt-get install autoconf
$ sudo apt install mpich
$ sudo apt install libconfig-dev
$ sudo apt install libnetcdf-dev
```

EPREM currently does not support serial operation (although it is possible in certain circumstances); `configure.sh` will do its best to find suitable MPI compilers without the need for explicitly setting `CC=..` and `CXX=...`, but if set-up fails, you may try doing so.

Users familiar with the GNU Autotools are welcome to bypass `setup.sh` and directly run
```
./configure OPTIONS && make && make install
```
with whichever `OPTIONS` they require.

Finally, to verify that the installation was successful, run one of the examples, such as: 

```
mpirun -n 2 eprem-latest cone.ini 
```
