---
name: cloudguard-kubernetes-image-assurance
description: Onboard a Kubernetes cluster to CloudGuard, turn on image assurance, runtime protection and admission control, and read image vulnerabilities.
api: CloudGuard Workload Protection API
generated: '2026-09-05'
method: generated
source: openapi/cloudguard-onboarding-openapi.yml, openapi/cloudguard-workload-protection-openapi.yml
base_url: https://api.dome9.com
operations:
  - KubernetesAccount_Post_post_/v2/kubernetes/account
  - KubernetesAccount_GetAll_get_/v2/kubernetes/account
  - KubernetesAccount_Get_get_/v2/kubernetes/account/{id}
  - KubernetesAccount_EnableImageAssurance_post_/v2/kubernetes/account/{id}/imageAssurance/enable
  - KubernetesAccount_DisableImageAssurance_post_/v2/kubernetes/account/{id}/imageAssurance/disable
  - KubernetesAccount_EnableRuntimeProtection_post_/v2/kubernetes/account/{id}/runtimeProtection/enable
  - KubernetesAccount_EnableAdmissionControl_post_/v2/kubernetes/account/{id}/admissionControl/enable
  - KubernetesAccount_DisableAdmissionControl_post_/v2/kubernetes/account/{id}/admissionControl/disable
  - KubernetesAccount_GetAccountSummary_get_/v2/kubernetes/account/{id}/accountSummary
  - KubernetesAccount_GetAgentSummary_get_/v2/kubernetes/account/{id}/agentSummary
  - KubernetesAccount_GetAccountAgentStatus_get_/v2/kubernetes/account/accountAgentStatus
  - KubernetesImageAssurance_GetImage_get_/v2/kubernetes/imageAssurance/image
  - KubernetesImageAssurance_GetClusterPodAndImages_get_/v2/kubernetes/imageAssurance/account/{clusterId}/podsImages
  - KubernetesAccount_Delete_delete_/v2/kubernetes/account/{id}
---

# Kubernetes workload protection

HTTP Basic with the V2 API key id / secret, base `https://api.dome9.com/v2/`.

## Steps

1. **Register the cluster.** `POST /v2/kubernetes/account`
   (`KubernetesAccount_Post_post_/v2/kubernetes/account`). Check `GET /v2/kubernetes/account` first —
   no idempotency key exists, so a repeat POST registers a second cluster record. If duplicates do
   appear, `POST /v2/kubernetes/account/{id}/resolveMultipleOnboarding` is the published cleanup.
2. **Enable the capabilities you need**, each its own call:
   - `POST /v2/kubernetes/account/{id}/imageAssurance/enable`
   - `POST /v2/kubernetes/account/{id}/runtimeProtection/enable`
   - `POST /v2/kubernetes/account/{id}/admissionControl/enable`
   Image assurance and admission control each have a matching `/disable`, which is their reversal.
   **Runtime protection has an `enable` with no published `disable` operation** — do not assume you can
   turn it back off through this API.
3. **Confirm the agent is healthy.** `GET /v2/kubernetes/account/{id}/agentSummary`,
   `GET /v2/kubernetes/account/accountAgentStatus`, and
   `POST /v2/kubernetes/account/agentStatusReportCSV` for a CSV export
   (`application/octet-stream`). `GET /v2/kubernetes/account/{id}/accountSummary` gives the posture
   rollup.
4. **Read image risk.** `GET /v2/kubernetes/imageAssurance/image` for an image,
   `GET /v2/kubernetes/imageAssurance/account/{clusterId}/podsImages` for everything running in a
   cluster, `GET /v2/kubernetes/imageAssurance/image/podGroups` for where an image is deployed.
   Vulnerabilities are addressed by **CVE id**.
5. **Organise.** `PUT /v2/kubernetes/account/{id}/organizationalUnit` and the
   `organizationalUnit/move|moveAll|attach` operations place clusters in OUs; `null` means the root OU.

## Rules

- **Deprecated surface — check before you build.** These image-assurance operations carry
  `deprecated: true` in the published contract and should not be used in new work:
  `KubernetesImageAssurance_GetImageVulnerabilities_get_/v2/kubernetes/imageAssurance/image/vulnerabilities`
  and the whole `/v2/kubernetes/imageAssurance/policy` group (GET/POST/PUT/DELETE). Check Point
  publishes **no removal date and no Sunset header**, so plan the migration yourself.
- **Admission control blocks deployments.** Enabling it changes what the cluster will accept. Treat
  `admissionControl/enable` and any admission-policy write as a production change needing human
  approval.
- `DELETE /v2/kubernetes/account/{id}` removes the cluster from CloudGuard. No restore is published.
- No pagination, no idempotency, no published rate limits, no 4xx responses in the contract.
