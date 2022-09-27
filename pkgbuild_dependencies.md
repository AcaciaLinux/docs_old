# Branch package build dependency management

Branch package build dependencies get split up in 3 groups:

- `dependencies`

- `build_deps`

- `cross_deps` 

#### dependencies

These are the dependencies that get inserted into the `leaf.pkg` file inside the package and that are needed for the package to work at runtime.

#### build_deps

The build dependencies are needed for building the package, if you need a package at buildtime and runtime, you have to specify it here and at `dependencies`. The `branchbuildbot` does only install dependencies specified unter `build_deps` when building a release build.

#### cross_deps

This class of dependencies is needed for packages that can be built in using the `crosstools` toochain following a `crossbuild` call within the `leafclient`. If `cross_deps` is not specified and the packages builds the package as a cross build, the `build_deps` dependencies are used.

> **Note**
> 
> Getting `build_deps` and `cross_deps` right will make or break you package build file! `branch` does only install one of both sets:
> 
> - `releasebuild` - `rb`: `build_deps`
> 
> - `crossbuild` - `cb`: `cross_deps` if supplied, else `build_deps`.


