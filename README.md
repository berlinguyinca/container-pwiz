# Proteowizard msconvert Docker Buildfile

The first step in a metabolomics data processing workflow with Open
Source tools is the conversion to an open raw data format like
[mzML]:https://github.com/HUPO-PSI/mzML/ .

One of the main routes to mzML-formatted data is using Open Source converter
msconvert developed by the Proteowizard team (Chambers et al. 2012), 
which is one of the reference implementations for mzML. It can convert 
to mzML from Sciex, Bruker, Thermo, Agilent, Shimadzu, Waters 
and also the earlier file formats like mzData or mzXML.

Although Proteowizard was initially targeting LC/MS data, it can also readily 
convert GC/MS data for example from the Waters GCT Premier or Agilent instruments.

## Building the Docker image

Please note that for licensing reasons we can not include all required 
files in this repository. Please head over to http://proteowizard.sourceforge.net/downloads.shtml
and place the installer pwiz-setup-3.0.9098-x86.msi in this directory.
Also note that the build is known to fail with Docker-1.9, make sure to use Docker-1.10 or above.

`docker build --tag="phnmnl/pwiz:latest" .`

## Using the Docker image

After building the image, the conversion can be started with e.g. 

`docker run -v $PWD:/data:rw phnmnl/pwiz:latest /data/neg-MM8_1-A,1_01_376.d -o /data/ --mzML`

The currently tested vendor formats are:

* mzXML: `docker run -it -v $PWD:/data phnmnl/pwiz:3.0.9098-0.1 threonine_i2_e35_pH_tree.mzXML`
* Bruker *.d: `docker run -it -v $PWD:/data phnmnl/pwiz:3.0.9098-0.1 neg-MM8_1-A,1_01_376.d`

## Galaxy usage

A rudimentary Galaxy node description is included as `msconvert.xml`, 
it was obtained from the `msconvert.ctd` using 
`python CTD2Galaxy/generator.py -i /vol/phenomenal/vmis/docker-pwiz/msconvert.ctd -m sample_files/macros.xml -o /vol/phenomenal/vmis/docker-pwiz/msconvert.xml`










