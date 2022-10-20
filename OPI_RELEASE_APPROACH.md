# OPI Release Approach

OPI will eventually release some artifacts around the work being done in the
project. This document details *how* the artifacts are released, and how it
relates to the form the project takes, meaning this document is the result of a
[mailing list discussion](https://lists.opiproject.org/g/tsc/message/30)
around the OPI release process.

Specifically, the following three approaches were considered as becoming the
OPI Release Process:

1. Standards documents & Protobuf Models Specifications only

    * Need to verify models (even if this is manual effort)
    * Even if this is using companies' private labs and private DPUs and IPUs
    * Similar to CSI, FMDS, T11, T10, etc.

2. Protobuf Specs + Reference releases

    * POC/Reference
        * Examples:  OPI-Nvidia bridge on BlueField and OPI-Intel bridge on MEV
          and OPI-Marvell bridge on Octeon
    * Can be based on OPI-SPDK bridge I built
    * Releases are un-versioned and just examples
    * Tools and Clients Examples from some open-source projects: Mockup, CLI
      Client
    * Similar to Redfish

3. Full Community Release

    * Testing
    * Issue tracking & support
    * Release tracking
    * Release cadence
    * Release content
    * CI/CD and testing
    * Deploy/installation
    * Similar to SONiC

## Proposed Release Approach

This document proposes OPI will start by releasing an API in the form of
protobuf specs and a reference architecture. **The reference architecture is
not meant to be used in production.** Note this chosen approach is option
number 2 from the above list of choices.

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
  * sZTP code, including a custom client
* A Container Storage Interface (CSI) library, client and helpful
  utilities called [goopicso](https://github.com/opiproject/goopicsi)

OPI is tracking work in the following specific areas, which will each contain
pieces of the above release artifacts:

* AI/ML
* Networking
* Storage
* Security

### Working Group Specific Release Items

* [Storage](https://github.com/opiproject/opi-api/tree/main/storage#deliverables)

The above example allows for vendors to release their own bindings for
the APIs as well. For example:

* OPI AMD/Pensando
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
