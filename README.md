# CloudGuard (cloudguard)

Check Point CloudGuard is a Cloud Native Application Protection Platform (CNAPP) covering cloud security posture management (CSPM), cloud workload protection (CWPP), code security, cloud network security, WAF/AppSec, and intelligence/CDR. The public CloudGuard REST API (originally Dome9 v2) is used to onboard AWS, Azure, GCP, Alibaba, Oracle, Kubernetes, and on-prem accounts; run compliance and posture assessments; list and manage findings/alerts; configure IAM safety, network policies, and notifications.

**APIs.json:** [apis.yml](https://raw.githubusercontent.com/api-evangelist/cloudguard/refs/heads/main/apis.yml)

## Scope

- **Type:** Index
- **x-type:** company
- **Company:** Check Point Software Technologies
- **Position:** Consumer
- **Access:** 3rd-Party

## Tags

Check Point, CNAPP, Cloud Security, Compliance, CSPM, CWPP, Posture Management

## APIs

### CloudGuard CNAPP REST API
The CloudGuard CNAPP REST API (formerly Dome9 v2) for cloud account onboarding, posture assessments, compliance rulesets, findings, alerts, IAM safety, and network security configuration. Auth uses HTTP Basic with an API key and secret.

- [Documentation](https://docs.cgn.portal.checkpoint.com/reference)
- [OpenAPI](https://api.dome9.com/v2/swagger.json)
- [Authentication](https://sc1.checkpoint.com/documents/CloudGuard_Dome9/Documentation/API-Authentication.html)
- [Terraform Provider](https://registry.terraform.io/providers/dome9/dome9/latest/docs)

### CloudGuard Workload Protection (CWPP)
Kubernetes admission control, image assurance / CI scanning, runtime protection, and serverless function security.

### CloudGuard Code Security (Spectral)
Developer-first SAST, IaC scanning, secrets detection, and SCA integrated into CI/CD pipelines via CLI and API.

### CloudGuard WAF (AppSec)
Contextual ML-based protection for web apps and APIs.

### CloudGuard Network Security
Cloud-native firewalling and threat prevention with management APIs for gateway provisioning and rule management.

## Common Properties

- [Website](https://www.checkpoint.com/cloudguard/)
- [Documentation](https://docs.cgn.portal.checkpoint.com/)
- [Developer Portal](https://docs.cgn.portal.checkpoint.com/reference)
- [Support](https://support.checkpoint.com/)
- [Status](https://status.dome9.com/)
- [JSON-LD](json-ld/cloudguard-context.jsonld)
- [Spectral](rules/cloudguard-rules.yml)
- [Naftiko Capabilities](capabilities/cloudguard-capabilities.yml)

## Maintainers

- **FN:** Kin Lane
- **Email:** kinlane@gmail.com
