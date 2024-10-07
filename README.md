# Pomona College Ondemand RStudio Server

An interactive app designed for Pomona College Ondemand Rstudio server.

This was configured to reduce complexity and allow `rstudio-server` and `r` version to be dynamicly picked up.

## Prerequisites

This Batch Connect app requires the following software be installed on the
**compute nodes** that the batch job is intended to run on (**NOT** the
OnDemand node):

- [Lmod] 6.0.1+ or any other `module restore` and `module load <modules>` based
  CLI used to load appropriate environments within the batch job before
  launching the RStudio Server.
- [R] 3.3.2+ (earlier versions are untested but may work for you)
- [RStudio Server] 1.0.136+ (earlier versions are untested by may work for you)

## Installation

I am using rstudio-server rpm to reduce complexity of installing too many dependency on the node.

```sh
name="rstudio-server"
version="2022.12.0+353"
wget https://download2.rstudio.org/server/rhel8/x86_64/rstudio-server-rhel-$(echo $version | tr + -)-x86_64.rpm
mkdir $version
rpmdev-extract rstudio-server-rhel-$(echo $version | tr + -)-x86_64.rpm
mkdir -p $HPC_SOFTWARE/$name/$version
cp -Rv rstudio-server-$version-1.x86_64/usr/lib/rstudio-server/* $HPC_SOFTWARE/$name/$version
```

## Apptainer usage
Copy the `r.def` to your machine.
```sh
#load apptainer
module load apptainer
#build the apptainer
#modify the r.def if you need specific library or a different OS
apptainer build r.sif r.def
```