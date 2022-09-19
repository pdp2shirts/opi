# OPI Release Approach

OPI will eventually release some artifacts around the work being done in the
project. This document details *how* the artifacts are released, and how it
relates to the form the project takes, meaning this document is the result of a
[mailing list discussion](https://lists.opiproject.org/g/tsc/message/30)
around the OPI release process.

## Proposed Release Approach

This document proposes OPI will start by releasing an API in the form of
protobuf specs and a reference architecture. **The reference architecture is
not meant to be used in production.**

The details of what this will look like are as follows:

* The protobuf files themselves.
  * Some language specific bindings for those files. For example, bindings for
    C++, golang, python, and Rust.
  * Documentation around the protobuf files
* A reference implementation which implements the protobuf files
  * gRPC server code which incorporates the protobuf files.
  * Implementation specific examples of the APIs themselves.
    * SPDK for the Storage APIs
    * strongSwan for Security IPsec APIs
    * XDP program for the Security Firewall programs
  * gRPC client code to work with the server code
  * CLI based on the gRPC client code
* Code related to provisioning and lifecycle:
  * OTEL integration poins
  * sZTP code which may include a custom client
* A Container Storage Interface (CSI) library, client and helpful
  utilities called [goopicso](https://github.com/opiproject/goopicsi)

OPI is tracking work in the following specific areas, which will each contain
pieces of the above release artifacts:

* AI/ML
* Networking
* Storage
* Security

The above example allows for vendors to release their own bindings for
the APIs as well. For example:

* OPI Intel
* OPI Marvell
* OPI NVIDIA

The above list is not meant to be inclusive of all DPU and IPU vendors,
but merely an example of some vendors showing how they could release
bindings for OPI APIs.

We also propose these bindings are created in repositories in the
[OPI Github](https://github.com/opiproject). However, if a vendor wants to
use their own GitHub organization for the repository, they are free to do
that as well.

We will version the releases using [semantic versioning](https://semver.org).
