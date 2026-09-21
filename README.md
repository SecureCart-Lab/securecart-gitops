# SecureCart GitOps Repository

This repository is the **desired-state repository** for the SecureCart lab. Argo CD reconciles these files into EKS. The application CI pipeline builds/scans/signs an image, pushes it to ECR, and changes only the image reference in this repository. Routine application deployment is therefore performed by Argo CD rather than `kubectl apply` from CI.

## Layout

- `charts/securecart/` — SecureCart + PostgreSQL Helm chart, RBAC, NetworkPolicies and ServiceMonitor.
- `argocd/applications/` — Argo CD Applications for storage, Kyverno, Vault, monitoring, Loki, Alloy, Falco, policies and SecureCart.
- `platform/` — values/manifests for free self-hosted platform components.
- `policies/` — Kyverno policies and safe negative-test manifests.

## Before first sync

1. Replace every `REPLACE_ME` placeholder with your GitHub owner or ECR account/repository value.
2. Do **not** commit passwords, Slack webhooks, Vault root/unseal material, tokens, or Kubernetes Secret values.
3. Create runtime secrets out of band with the helper in the engineering repository.
4. Apply Argo applications in the order documented in `securecart-devsecops/README.md`; CRD-producing charts must exist before CRs such as `PrometheusRule`, `AlertmanagerConfig`, and Kyverno `ClusterPolicy`.

## Pinned platform chart versions

The lab pins chart versions so a student receives a reproducible baseline rather than silently installing a future incompatible chart. Review and test upgrades through pull requests before changing the pins.
