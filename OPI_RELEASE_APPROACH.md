# OPI Release Approach

OPI will eventually release some artifacts around the work being done in the
project. What those artifacts are is still being discussed. However, *how*
they are released, and how it relates to the form the project takes, is
something worth documenting. This document is the result of a
[mailing list discussion](https://lists.opiproject.org/g/tsc/message/30)
around the OPI release process.

## Proposed Release Approach

This document proposes OPI will start by releasing an API in the form of
protobuf specs and a reference architecture not meant to be used in
production. The details of what this will look like are as follows:

* The protobuf files themselves.
  * Language specific bindings for those files. For example, bindings for
    C++, golang, python, and Rust.
  * Documentation around the protobuf files
* A reference implementation which implements the protobuf files
  * gRPC server code which incorporates the protobuf files.
  * Implementation specific examples of the APIs themselves.
    * SPDK for the Storage APIs
    * strongSwan for Security IPsec APIs
    * XDP program for the Security Firewall programs
  * gRPC client code to work with the server code

The above example allows for vendors to release their own bindings for
the APIs as well. For example:

* OPI Intel
* OPI Marvell
* OPI NVIDIA

The above list is not meant to be inclusive of all DPU and IPU vendors,
but merely an example of some vendors showing how they could release
bindings for OPI APIs.

We also propose these bindings are created in repositories in the
[OPI Github](https://github.com/opiproject).

We will version the releases using [semantic versioning](https://semver.org).
