# Advanced Cluster Management PolicyGenerator Example

This repo is an example of how to leverage the RHACM `policygenerator` tool to create custom policies.

In `base` there are a series of manifests with a default, baseline configuration.

In `overlays` there are sub directories represeting `prod`, `stg` (stage) and `dev`. Each has a `kustomization.yaml` making some change to the `base` object

`policygenerator.yaml` contains the base configuration for generating the policies with the `policygenerator` cli tool. It:

* Dynamically generates instances of namespace-scoped resources to specific namespaces (reducing boilerplate).
* Renders the manifests specific for each environment type.
* Assigns the respective binding to the ManagedClusterSets objects representing these environments.


## Instructions

```bash
policygenerator policygenerator.yaml > policies.yaml
oc apply -f policies.yaml
```

By default the policies are set to `inform` only.