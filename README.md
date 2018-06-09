# build_containers [![Build Status](https://drone.jonnrb.com/api/badges/jon/build_containers/status.svg?branch=master)](https://drone.jonnrb.com/jon/build_containers)

## _Containers I use to build stuff_

So I recently (about 10 minutes ago) found out about multi-stage container
builds and this totally changes the game for me. I used to be a lazy person
and just bundle the container with all the build artifacts. Then I got a little
sophisticated and started building a container *inside* another container, but
this is just a hacky multi-stage build so #!$@ that!

Here's what I've got so far:

- `bazel_cc`: A recent Linux distro (Ubuntu Xenial) with a recent Bazel version
  (0.9.0) and a recent version of gcc and g++ (7). Just add your source to
  `/src`, build your `cc_binary` (either fully static or in a distroless image),
  and ship!

  NOTE: Run `dbazel` instead (to use `--batch` which speeds things up)
