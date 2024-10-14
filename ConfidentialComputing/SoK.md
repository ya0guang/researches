# SoK of CC

## Confidential Containers

- [Google Cloud](https://cloud.google.com/kubernetes-engine/docs/how-to/confidential-gke-nodes)
- [CC-API](https://github.com/cc-api)
- [Confidential Containers](https://github.com/confidential-containers)
- [inclavare-containers](https://github.com/inclavare-containers)
- [contrast](https://github.com/edgelesssys/contrast)
- [Azure Confidential Containers](https://learn.microsoft.com/en-us/azure/confidential-computing/confidential-containers)

### Questions

- How does CC handles secrets (e.g., in configuration)? Tokens, ssh keys, etc.
- How runtime policy is used? How it's been handled in CC?
- Is (Kata) Agent interface secure?

### Features (might be Potential Problems)

- Service Mesh
  - [Contrast RFC001](https://github.com/edgelesssys/contrast/blob/main/rfc/001-service-mesh.md)
  - Traffic Routing Correct?
- Metrics
  - [Contrast RFC003](https://github.com/edgelesssys/contrast/blob/main/rfc/003-coordinator-metrics.md)
  - What information is and should (not) be collected? This relates to the threat model.
- Recovery
  - [Contrast RFC004](https://github.com/edgelesssys/contrast/blob/main/rfc/004-recovery.md)
  - This sounds like a very dangerous feature. How to defend against availability attacks and replay attacks?
- Secret Persistence
  - [Contrast RFC007](https://github.com/edgelesssys/contrast/blob/main/rfc/007-workload-secrets.md)
  - [Coco Trusted Storage Issue](https://github.com/confidential-containers/confidential-containers/issues/123)
  - [Coco Secure Storage (Documentation)](https://github.com/confidential-containers/guest-components/blob/main/confidential-data-hub/docs/SECURE_STORAGE.md)
  - Replay attack?
- Reference Value Generation
- Sidecar Containers
