# OPI Project — "Abstraction" Release (v0.1.0)

**Date:** 2026-05-08
**Codename:** Abstraction
**Release Manifest:** [`opi-release.json`](./opi-release.json)
**GitHub Org:** [github.com/opiproject](https://github.com/opiproject)
**Website:** [opiproject.org](https://opiproject.org)

---

## Overview

This is the first coordinated release of the
**Open Programmable Infrastructure (OPI) Project**,
codenamed **"Abstraction"**.

The name reflects the core mission of this release: to establish a
vendor-neutral, hardware-agnostic API abstraction layer across all DPU/IPU
capabilities — so that any workload, orchestrator, or platform can program
any DPU without hardware-specific code.

This release pins a specific tag and commit across 22 participating
repositories, spanning API definitions, reference bridge implementations,
vendor bridges, client tooling, Kubernetes integrations, provisioning
infrastructure, and observability tooling.

---

## What is OPI?

OPI defines open, portable gRPC/protobuf APIs that abstract DPU/IPU hardware
capabilities across vendors. An application or orchestration platform targeting
OPI APIs can work with any compliant DPU — NVIDIA BlueField, Intel MEV, Marvell
OCTEON, or MangoBoost — without hardware-specific code.

---

## A Note on Terminology: Capability Areas vs. Blueprints

This release uses two distinct concepts that are intentionally kept separate:

### Capability Areas

A **Capability Area** describes which OPI functional domain a repository
contributes to — what it technically enables. The four capability areas in
this release are:

- **Storage Offload** — NVMe-oF frontend/backend, VirtIO, encryption,
  QoS, AIO volumes, CSI
- **Secure Networking** — EVPN gateway, IPsec IKE + ESP datapath offload,
  CNI/Kubernetes integration
- **DPU Inventory & Telemetry** — SMBIOS-based hardware inventory,
  OpenTelemetry metrics and traces
- **DPU Provisioning & Lifecycle** — sZTP (RFC 8572), Redfish,
  Ansible lifecycle automation

Every repository in this release manifest carries a `keywords` field in
[`opi-release.json`](./opi-release.json) describing its technical domain.

### OPI Blueprints

An **OPI Blueprint** is something much more specific. Per the
[OPI Blueprint Framework](https://github.com/opiproject/opi/blob/main/Docs/blueprint_framework.md),
a Blueprint is a **fully documented, partner-attributed, production-grade
deployment pattern** that an enterprise customer or systems integrator could
replicate. It must include:

- A reference architecture diagram
- A validated bill of materials (BOM) with specific hardware and software versions
- A deployment guide with IaC artifacts (Terraform, Ansible, Helm, etc.)
- A use case narrative aimed at IT decision-makers, not just developers
- Validated test results
- Clear partner/integrator attribution and a path to professional services

A Blueprint answers *"how do I deploy this at my company?"* — not just
*"does it work?"*. Repos that have been validated as part of an official
Blueprint carry a `blueprints` field in the release manifest. Repos that have
not are listed with an empty `blueprints` array, regardless of how capable
they are technically.

**OPI currently has one official Blueprint** — see below.

---

## Official Blueprint: Kubernetes Network Function Offload

**Partners:** Intel · Marvell · Red Hat · F5 / NGINX
**Hardware:** Intel IPU E2100, Marvell OCTEON DPU
**Software:** Red Hat OpenShift, F5 NGINX
**Status:** Official

This Blueprint demonstrates end-to-end Kubernetes-native network function
offload to DPU/IPU hardware using OPI APIs, with Red Hat OpenShift as the
orchestration layer and F5 NGINX as the application delivery controller.
It is the first OPI Blueprint to meet the full framework requirements:
reference architecture, BOM, deployment guide, IaC artifacts, and validated
test results with multi-vendor partner attribution.

The following repositories from this release have been validated as part
of this Blueprint:

| Repository | Tag | Role in Blueprint |
| --- | --- | --- |
| [opi-api](https://github.com/opiproject/opi-api) | v1.0.0 | Defines the EVPN and networking gRPC API contracts |
| [opi-evpn-bridge](https://github.com/opiproject/opi-evpn-bridge) | v0.2.0 | EVPN gateway reference implementation (FRR) |
| [opi-intel-bridge](https://github.com/opiproject/opi-intel-bridge) | v0.2.0 | Intel IPU E2100 vendor implementation |
| [opi-marvell-bridge](https://github.com/opiproject/opi-marvell-bridge) | v0.1.2 | Marvell OCTEON vendor implementation |
| [opi-gateway-evpn-cni](https://github.com/opiproject/opi-gateway-evpn-cni) | v1.0.0 | Kubernetes CNI plugin connecting pods to EVPN gateway |
| [opi-cni](https://github.com/opiproject/opi-cni) | v1.0.0 | Generic OPI CNI integration for Kubernetes |
| [sessionOffload](https://github.com/opiproject/sessionOffload) | v1 | Session offload API for datapath acceleration |
| [godpu](https://github.com/opiproject/godpu) | v0.2.0 | Go CLI used for Blueprint validation |
| [pydpu](https://github.com/opiproject/pydpu) | v0.2.1 | Python CLI used for Blueprint validation |
| [opi-poc](https://github.com/opiproject/opi-poc) | v1.0.0 | Integration test suite and CI PoC compose stack |

---

## Repository Summary Table

| Repository | Tag | Commit | Capability Area(s) | Type | In Blueprint |
| --- | --- | --- | --- | --- | --- |
| [opi-api](https://github.com/opiproject/opi-api) | v1.0.0 | `0b58e48b` | Storage Offload, Secure Networking, DPU Inventory & Telemetry | API Definitions | ✅ |
| [opi-poc](https://github.com/opiproject/opi-poc) | v1.0.0 | `3118ff80` | All | Integration Testing | ✅ |
| [opi-smbios-bridge](https://github.com/opiproject/opi-smbios-bridge) | v0.1.2 | `85e800cf` | DPU Inventory & Telemetry | Bridge | — |
| [opi-mangoboost-bridge](https://github.com/opiproject/opi-mangoboost-bridge) | v1.0.0 | `c086acf5` | Storage Offload | Vendor Bridge | — |
| [spdk](https://github.com/opiproject/spdk) | v24.01 | `0b102908` | Storage Offload | Container Packaging | — |
| [opi-spdk-bridge](https://github.com/opiproject/opi-spdk-bridge) | v0.1.1 | `88edfc9e` | Storage Offload | Bridge | — |
| [opi-intel-bridge](https://github.com/opiproject/opi-intel-bridge) | v0.2.0 | `83a34699` | Storage Offload, Secure Networking, DPU Inventory & Telemetry | Vendor Bridge | ✅ |
| [opi-evpn-bridge](https://github.com/opiproject/opi-evpn-bridge) | v0.2.0 | `5440fb9f` | Secure Networking | Bridge | ✅ |
| [sztp](https://github.com/opiproject/sztp) | v0.2.0 | `8ae1e7d5` | DPU Provisioning & Lifecycle | Provisioning | — |
| [godpu](https://github.com/opiproject/godpu) | v0.2.0 | `eb709487` | Storage Offload, Secure Networking, DPU Inventory & Telemetry | Client Tooling | ✅ |
| [opi-strongswan-bridge](https://github.com/opiproject/opi-strongswan-bridge) | v0.1.1 | `98602d8c` | Secure Networking | Bridge | — |
| [otel](https://github.com/opiproject/otel) | v1.0.0 | `d7b81b0b` | DPU Inventory & Telemetry | Observability | — |
| [pydpu](https://github.com/opiproject/pydpu) | v0.2.1 | `3f4b838a` | Storage Offload, Secure Networking, DPU Inventory & Telemetry | Client Tooling | ✅ |
| [ansible-opi-dpu](https://github.com/opiproject/ansible-opi-dpu) | v1.0.0 | `42d5399b` | DPU Provisioning & Lifecycle | Automation | — |
| [opi-nvidia-bridge](https://github.com/opiproject/opi-nvidia-bridge) | v0.1.2 | `16632dfb` | Storage Offload, Secure Networking, DPU Inventory & Telemetry | Vendor Bridge | — |
| [opi-marvell-bridge](https://github.com/opiproject/opi-marvell-bridge) | v0.1.2 | `a2338007` | Storage Offload, Secure Networking, DPU Inventory & Telemetry | Vendor Bridge | ✅ |
| [opi-gateway-evpn-cni](https://github.com/opiproject/opi-gateway-evpn-cni) | v1.0.0 | `a2207f82` | Secure Networking | CNI Plugin | ✅ |
| [gospdk](https://github.com/opiproject/gospdk) | v1.0.0 | `98d71122` | Storage Offload | Shared Library | — |
| [opi-prov-life](https://github.com/opiproject/opi-prov-life) | v1.0.0 | `c18ec9e1` | DPU Provisioning & Lifecycle | Working Group Docs | — |
| [opi-cni](https://github.com/opiproject/opi-cni) | v1.0.0 | `8751c724` | Secure Networking | CNI Plugin | ✅ |
| [sztpd](https://github.com/opiproject/sztpd) | 0.0.15 | `40c371ea` | DPU Provisioning & Lifecycle | Container Packaging | — |
| [sessionOffload](https://github.com/opiproject/sessionOffload) | v1 | `8708e583` | Secure Networking | API Definitions | ✅ |

> **Note:** Repositories showing `—` for tag/commit have not yet cut a
> formal release tag. They participate in this release at their current HEAD.
> Future releases will require all repositories to carry a tag.

---

## Highlights by Capability Area

### Storage Offload

The OPI Storage API (`opi_api.storage.v1`) defines a comprehensive set of
gRPC services covering the full NVMe-oF stack: frontend NVMe, VirtIO block
and SCSI, middleend encryption and QoS, remote NVMe controllers, and generic
AIO/Null volumes.

- **`opi-spdk-bridge` v0.1.1** is the reference implementation, translating
  all storage gRPC services to SPDK JSON-RPC. It is the canonical backend
  used in CI and PoC validation.
- **`spdk` v24.01** provides the containerized SPDK engine used by the bridge
  and integration tests.
- **`gospdk`** provides the reusable Go SPDK JSON-RPC client library,
  covering NVMf, LVol, BDev, Crypto, and Accel subsystems.
- Vendor storage bridges: **`opi-nvidia-bridge` v0.1.2**,
  **`opi-intel-bridge` v0.2.0**, **`opi-marvell-bridge` v0.1.2**,
  **`opi-mangoboost-bridge`**, and
  each implement the same storage gRPC surface against
  their respective DPU SDKs.

### Secure Networking

The OPI Networking API (`opi_api.network.evpn_gw.v1alpha1`) models an EVPN
gateway with VRFs, Logical Bridges, Bridge Ports, and SVIs. The complementary
`sessionOffload` API covers ESP datapath offload.

- **`opi-evpn-bridge` v0.2.0** is the reference implementation backed by
  FRRouting (FRR). v0.2.0 adds pagination, TLS options, Redis-backed state
  persistence, and richer integration tests.
- **`opi-strongswan-bridge` v0.1.1** bridges the OPI IPsec gRPC API to the
  strongSwan IKE daemon via the vici protocol. The combined strongSwan +
  sessionOffload pattern is the recommended OPI IPsec architecture:
  strongSwan manages the control plane; the DPU handles the data plane.
- **`opi-gateway-evpn-cni`** is a Kubernetes CNI plugin (Multus-compatible)
  that calls the EVPN bridge gRPC to create BridgePorts for xPU VFs attached
  to pods.
- **`opi-cni`** provides a broader Kubernetes CNI integration layer for
  OPI-managed DPU/IPU network functions.
- **`sessionOffload` v1** defines the session offload API for
  hardware-accelerating TCP/UDP/IPsec ESP datapath flows directly on DPU
  hardware.

### DPU Inventory & Telemetry

The OPI Inventory API (`opi_api.inventory.v1`) exposes DPU/IPU hardware
information (CPU, memory, PCIe, firmware) via a standard gRPC interface.

- **`opi-smbios-bridge` v0.1.2** is the reference implementation, reading
  SMBIOS tables via dmidecode and the ghw Go library.
- **`otel`** extends inventory with live telemetry — collecting CPU usage,
  memory, storage I/O, network throughput, and Redfish thermal sensor data via
  the OpenTelemetry collector pipeline, with traces exported to Zipkin/Jaeger.

### DPU Provisioning & Lifecycle

- **`sztp` v0.2.0** implements RFC 8572 Secure Zero Touch Provisioning
  end-to-end: a Go agent, a wn-sztpd-1 bootstrap server client, and a DHCP
  option 143 redirect mechanism for zero-touch DPU onboarding.
- **`sztpd` 0.0.15** packages the wn-sztpd-1 bootstrap server daemon as a
  container for use in OPI lab and production sZTP deployments.
- **`ansible-opi-dpu` v1.0.0** provides Ansible roles and playbooks for
  automating DPU/IPU provisioning, configuration, and lifecycle management at
  scale.
- **`opi-prov-life`** serves as the working group documentation hub,
  covering sZTP, PXE, Redfish, and lifecycle management blueprints and
  architecture specs.

---

## Client Libraries

OPI provides first-class client libraries in two languages so that
orchestration platforms and test frameworks can interact with any OPI-compliant
bridge without writing raw gRPC boilerplate:

- **`godpu` v0.2.0** — Go CLI and library. Supports `storage`, `evpn`,
  `ipsec`, and `inventory` sub-commands. Used in all OPI CI pipelines.
- **`pydpu` v0.2.1** — Python client library and CLI. Python equivalent of
  godpu. Published to PyPI.

---

## Vendor DPU/IPU Support Matrix

| Vendor | Hardware | Bridge Repo | Storage Offload | Secure Networking | DPU Inventory | Provisioning |
| --- | --- | --- | :---: | :---: | :---: | :---: |
| NVIDIA | BlueField DPU | opi-nvidia-bridge v0.1.2 | ✅ | ✅ | ✅ | — |
| Intel | MEV / IPU | opi-intel-bridge v0.2.0 | ✅ | ✅ | ✅ | — |
| Marvell | OCTEON DPU | opi-marvell-bridge v0.1.2 | ✅ | ✅ | ✅ | — |
| MangoBoost | DPU | opi-mangoboost-bridge | ✅ | — | — | — |
| Reference (SPDK) | Software | opi-spdk-bridge v0.1.1 | ✅ | — | — | — |
| Reference (FRR) | Software | opi-evpn-bridge v0.2.0 | — | ✅ | — | — |
| Ref (strongSwan) | Software | opi-strongswan-bridge v0.1.1 | — | ✅ | — | — |
| Reference (SMBIOS) | Software | opi-smbios-bridge v0.1.2 | — | — | ✅ | — |

---

## Repositories Without a Release Tag

The following repositories participate in this release at their current
HEAD but have not yet cut a formal tag. The OPI TSC recommends these repos
establish a release tagging process before v0.2.0:

`otel`, `opi-gateway-evpn-cni`, `gospdk`, `opi-prov-life`, `opi-cni`,
`smbios-validation-tool`, `spdk-csi`

---

## Excluded Repositories

The following repositories are part of the `opiproject` GitHub organization
but are intentionally excluded from this release manifest (infrastructure,
governance, and website repos):

`dpu-operator`, `opi`, `lab-private`, `actions`, `lab`, `artwork`, `opiproject.org`

---

## Getting Started

To get started with OPI, the recommended entry points are:

1. **API definitions** — clone [`opi-api`](https://github.com/opiproject/opi-api)
   or consume from the [Buf Schema Registry](https://buf.build/opiproject/opi-api)
2. **Reference PoC** — clone [`opi-poc`](https://github.com/opiproject/opi-poc)
   and run `docker compose up` to spin up a full local OPI stack backed by
   SPDK, FRR, and strongSwan
3. **CLI client** — install [`godpu`](https://github.com/opiproject/godpu)
   (`go install github.com/opiproject/godpu@latest`) or
   [`pydpu`](https://github.com/opiproject/pydpu) (`pip install pydpu`)
4. **Vendor bridge** — pick the bridge matching your DPU hardware and
   follow its README
5. **Blueprint** — see the
   [Kubernetes Network Function Offload](#official-blueprint-kubernetes-network-function-offload)
   section above for the first end-to-end, production-grade OPI deployment
   pattern

---

## Links

- Website: [https://opiproject.org](https://opiproject.org)
- GitHub: [https://github.com/opiproject](https://github.com/opiproject)
- Blueprint Framework: [opi/Docs/blueprint_framework.md](https://github.com/opiproject/opi/blob/main/Docs/blueprint_framework.md)
- Mailing list / community: see [opi](https://github.com/opiproject/opi) main repo
- Release manifest (machine-readable): [`opi-release.json`](./opi-release.json)
