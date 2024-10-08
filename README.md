# The Libstorage-ng Testing Image

[![CI](https://github.com/yast/ci-libstorage-ng-container/actions/workflows/ci.yml/badge.svg?branch=master)](
https://github.com/yast/ci-libstorage-ng-container/actions/workflows/ci.yml)
[![OBS](https://github.com/yast/ci-libstorage-ng-container/actions/workflows/submit.yml/badge.svg)](https://github.com/yast/ci-libstorage-ng-container/actions/workflows/submit.yml)

This git repository contains the configuration used to build the docker
image used for [GitHub Actions](https://docs.github.com/en/actions).
The resulting docker image is available at https://registry.opensuse.org/.

## Automatic Rebuilds

- The image is rebuilt whenever a commit it pushed to the `master` branch.
- The [submit.yml](./.github/workflows/submit.yml)
  GitHub Action commits the configuration to the [YaST:Head/ci-libstorage-ng-container](
  https://build.opensuse.org/package/show/YaST:Head/ci-libstorage-ng-container)
  OBS project
- The OBS tracks the dependencies and rebuilds the image if any dependant package
  is updated.

## Triggering a Rebuild Manually

If for some reason the automatic rebuild do not work or it failed you can
trigger the rebuild in the OBS just like for the other regular packages.


## The Image Content

This image is based on the latest openSUSE Tumbleweed image, additionally
it contains the packages needed for building and running the
[libstorage-ng](https://github.com/openSUSE/libstorage-ng) tests.

## Building the Image Locally

### Using the OSC Tool

From the Git sources:

```sh
# you need the rubygem-yast-rake package installed
rake osc:build
```

From the OBS checkout:

```sh
# check it out if not already present
osc co YaST:Head/ci-libstorage-ng-container
cd YaST:Head/ci-libstorage-ng-container

# build it
osc build containers
```

### Using the Docker tool

️:warning: This approach is not 100% the same as building the image with `osc` described above.
The `osc` build injects some special modifications to allow building the image inside
the OBS build environment.

:information_source:️ You should prefer using the `osc` method if possible, use the `docker`
build only as a fallback when the `osc` build is not possible or does not work in your environment.

```sh
docker build -t ci-libstorage-ng-container-test -f package/Dockerfile package/
```
