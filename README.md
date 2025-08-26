# CoastRI-ROMS

## About the model

ROMS solves the free-surface, hydrostatic, flux form of the primitive equations over variable bathymetry using stretched terrain following in the vertical and orthogonal curvilinear coordinates in the horizontal. The finite volume grid is discretized on a staggered Arakawa C-grid. Detailed information about its governing equations, numerical discretization, algorithms, usage, and tutorials is available in the WikiROMS documentation portal at www.myroms.org/wiki.

The [ROMS website](https://www.myroms.org) contains documentation of the model and is the canonical source of truth for the model.  The [ROMS code repository](https://github.com/myroms/roms) is the canonical source of truth for the model, and where issues regarding the model should be raised.

All users of ROMS are encouraged to register and engage on the [ROMS Forum](https://www.myroms.org/forum/)

## About this repository

This is the Model Deployment Repository for the CoastRI deployment of the ROMS model. This repository contains a [spack environment](https://spack.readthedocs.io/en/latest/environments.html) manifest file ([`spack.yaml`](./spack.yaml)) that defines all the essential components of the model, including exact versions of the source code used.

## Support

[ACCESS-NRI](https://www.access-nri.org.au) supports deployment of the ROMS model for the Australian Research Community as part of it's involvement in the [CoastRI Initiative](https://www.coastri.org.au).


[ACCESS-NRI](https://www.access-nri.org.au) **DOES NOT** support ROMS, or the running of ROMS on `gadi`.  Any questions about ACCESS-NRI releases of ROM should be done through the [ACCESS-Hive Forum](https://forum.access-hive.org.au/). See the [ACCESS Help and Support topic](https://forum.access-hive.org.au/t/access-help-and-support/908) for details on how to do this.

Any questions about ROMS should be directed to the [ROMS Forum](https://www.myroms.org/forum/) or the [ANCOMS ROMS category](https://forum.access-hive.org.au/c/ancoms/roms/226) on the ACCESS-Hive Forum.

### Build

ACCESS-NRI is using [spack](https://spack.io), a build from source package manager designed for use with high performance computing.

Spack automatically builds all the components and their dependencies, producing model component executables. Spack already contains support for compiling thousands of common software packages. Spack packages for the components are defined in the [spack packages repository](https://github.com/ACCESS-NRI/spack_packages/).

CoastRI-ROMS is built and deployed automatically to `gadi` on NCI (see below). However it is possible to use spack to compile the model using the `spack.yaml` environment file in this repository. To do so follow the [instructions on for configuring spack on `gadi`](https://access-hive.org.au/getting_started/spack/).

Then clone this repository and run the following commands on `gadi`:
```bash
spack env create coastri-roms spack.yaml
spack env activate coastri-roms
spack install
```
to create a spack environment called `coastri-roms` and build all the components, the locations of which can be found using `spack find --paths`.

### Source code

The ROMS source code used to build the model is contained in a fork on the ACCESS-Community-Hub organisation

https://github.com/ACCESS-Community-Hub/roms

Contributions and engagement is welcome.

### Deployment

CoastRI-ROMS is deployed automatically when a new version of the [`spack.yaml`](./spack.yaml) file is committed to `main` or a dedicated `backport/VERSION` branch. All the CoastRI-ROMS components are built using `spack` on `gadi` and installed under the [`vk83`](https://my.nci.org.au/mancini/project/vk83) project in `/g/data/vk83`. It is necessary to be a member of [`vk83`](https://my.nci.org.au/mancini/project/vk83) project to use ACCESS-NRI deployments of CoastRI-ROMS

The deployment process also creates a GitHub release with the same tag. All releases are available under the [Releases page](https://github.com/ACCESS-NRI/CoastRI-ROMS/releases). Each release has a changelog and meta-data with detailed information about the build and deployment, including:

- paths on `gadi` to all executables built in the deployment process (`spack.location`)
- a `spack.lock` file, which is a complete build provenance document, listing all the components that were built and their dependencies, versions, compiler version, build flags and build architecture. It is also installable via spack similarly to the `spack.yaml`. 
- the environment `spack.yaml` file used for deployment

Additionally the deployment creates environment modulefiles, the [standard method for deploying software on `gadi`](https://opus.nci.org.au/display/Help/Environment+Modules). To view available CoastRI-ROMS versions:

```bash
module use /g/data/vk83/modules
module avail coastri-roms
```

It is necessary to [join the vk83 project on gadi@NCI](https://my.nci.org.au/mancini/project/vk83) to access these deployments.

For users of CoastRI-ROMS model configurations supported by ANCOMS, knowledge of the exact location of the model executables is not required. Model configurations will be updated with new model components when necessary.

For information on contributing your own fixes to the CoastRI-ROMS `spack.yaml`, see the [Hive Docs article](https://docs.access-hive.org.au/models/run-a-model/create-a-prerelease/) on creating a prerelease.
