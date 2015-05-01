![alt text](https://github.com/scarrazza/compressor/raw/master/res/compressor_logo.png "Logo Compressor")

A compression tool for Monte Carlo PDF sets.

If you use this code in a scientific publication, please cite http://arxiv.org/abs/1504.06469

## Download

Download the latest [release](https://github.com/scarrazza/compressor/releases) or clone the master development repository by running the following command:

```Shell
$ git clone https://github.com/scarrazza/compressor.git
```
## Installation

Compressor requires [LHAPDF6](http://lhapdf.hepforge.org/), [ROOT](http://root.cern.ch/) and [GSL](http://www.gnu.org/software/gsl/).
Download the code and compile using the configure script:

```Shell
$ cd compressor
$ ./configure --prefix=/path/to/install/location
$ make && make install
```
This operation will copy the bin/compressor binary to /usr/local/bin.

## Usage
### Running the code

After installing this package, the *compressor* program is available for the user.
```Shell
$ compressor --help
  usage: ./compressor [REP] [PDF prior name] [energy Q=1] [seed=0] [compress=1]
```

The first 2 arguments are required:
- *[REP]* -> the number of required compressed replicas
- *[PDF prior name]* -> the name of prior LHAPDF6 grid
- *[energy Q]* -> the input energy scale used for the compression algorithm (default = 1 GeV)
- *[seed]* -> the random number seed (default = 0)
- *[compress]* -> switches on/off minimization (default = 1)

### Output

After running *compressor* a folder with the prior set name will be created.
```Shell
$ compressor 100 1000rep
  ...
$ ls 1000rep/
  erf_compression.dat         # contains the erf. values for the compressed set
  erf_random.dat              # contains the erf. values for the random set
  replica_compression_100.dat # list of replicas from the prior determined by the algorithm
```

The script */bin/compressor_buildgrid* creates the compressed LHAPDF6 grid:
```Shell
$ ./compressor_buildgrid --help
  usage: ./compressor_buildgrid [prior set name] [compressed rep]
```

Finally, in order to generate the ERF plots place the */bin/compressor_validate.C* script in the output folder and run
```Shell
$ root -l compressor_validate.C
```
## Auxiliary tools

We provide tools for the computation of correlations in the *tools/* folder and script for the construction of CMC-PDFs in *cmctools/* folder.

## Contact Information

Maintainer: Stefano Carrazza (stefano.carrazza@mi.infn.it)
