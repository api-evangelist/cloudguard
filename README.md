# CloudGuard (cloudguard)

Check Point CloudGuard is a Cloud Native Application Protection Platform (CNAPP) that delivers cloud security posture management (CSPM), cloud workload protection (CWPP), code security, network security, and intelligence/CDR capabilities across AWS, Azure, GCP, Alibaba, Oracle, Kubernetes, and on-premises environments. The CloudGuard public REST API (originally Dome9) is used to onboard cloud accounts, run posture assessments, manage compliance bundles, retrieve findings, and configure policies and alerts.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/cloudguard/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/cloudguard/refs/heads/main/apis.yml)

## Scope

- **Type:** Index
- **Position:** Consumer
- **Access:** 3rd-Party

## Tags

- Check Point
- CNAPP
- Cloud Security
- Compliance
- CSPM
- CWPP
- Posture Management

## Timestamps

- **Created:** 2024-01-01
- **Modified:** 2026-04-26

## APIs

### CloudGuard CNAPP REST API

The CloudGuard CNAPP REST API (formerly Dome9 v2) is used to onboard AWS, Azure, GCP, Kubernetes, and on-premises accounts; create and run compliance/posture rulesets; retrieve security findings and alerts; manage IAM safety, network policies, and exclusions; and configure notifications and integrations. Authentication is via API key and secret over HTTP Basic.

- **Human URL:** [https://docs.cgn.portal.checkpoint.com/reference](https://docs.cgn.portal.checkpoint.com/reference)

#### Tags

- CNAPP
- Cloud Security
- Compliance
- Posture

#### Properties

- [Documentation](https://docs.cgn.portal.checkpoint.com/reference)
- [OpenAPI](https://api.dome9.com/v2/swagger.json) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Authentication](https://sc1.checkpoint.com/documents/CloudGuard_Dome9/Documentation/API-Authentication.html)
- [Terraform  Provider](https://registry.terraform.io/providers/dome9/dome9/latest/docs)
- [Postman Collection](collections/cloudguard.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/cloudguard.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### CloudGuard Workload Protection (CWPP) API

Workload protection capabilities exposed through the CloudGuard platform for Kubernetes admission control, image assurance/CI scanning, runtime protection, and serverless function security.

- **Human URL:** [https://sc1.checkpoint.com/documents/CloudGuard_Dome9/Documentation/Workload/Overview.htm](https://sc1.checkpoint.com/documents/CloudGuard_Dome9/Documentation/Workload/Overview.htm)

#### Tags

- Container Security
- CWPP
- Image Assurance
- Kubernetes

#### Properties

- [Documentation](https://sc1.checkpoint.com/documents/CloudGuard_Dome9/Documentation/Workload/Overview.htm)
- [Postman Collection](collections/cloudguard.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/cloudguard.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### CloudGuard Code Security (Spectral) API

CloudGuard Code Security (formerly Spectral) provides developer-first SAST, infrastructure-as-code scanning, secrets detection, and SCA via CLI and API integrations into CI/CD pipelines.

- **Human URL:** [https://docs.spectralops.io/](https://docs.spectralops.io/)

#### Tags

- Code Security
- Secrets Detection
- SAST

#### Properties

- [Documentation](https://docs.spectralops.io/)
- [Postman Collection](collections/cloudguard.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/cloudguard.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### CloudGuard WAF API

CloudGuard WAF (CloudGuard AppSec) protects web applications and APIs with contextual machine-learning-based threat prevention; the platform exposes management APIs for policy, asset, and event configuration.

- **Human URL:** [https://sc1.checkpoint.com/documents/CloudGuard_AppSec/Documentation/Default.htm](https://sc1.checkpoint.com/documents/CloudGuard_AppSec/Documentation/Default.htm)

#### Tags

- API Security
- WAF
- Web Application Firewall

#### Properties

- [Documentation](https://sc1.checkpoint.com/documents/CloudGuard_AppSec/Documentation/Default.htm)
- [Postman Collection](collections/cloudguard.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/cloudguard.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### CloudGuard Network Security API

CloudGuard Network Security delivers cloud-native firewalling and threat prevention with management APIs for gateway provisioning, rule management, and integrations with CI/CD pipelines.

- **Human URL:** [https://www.checkpoint.com/cloudguard/cloud-network-security/](https://www.checkpoint.com/cloudguard/cloud-network-security/)

#### Tags

- Cloud Firewall
- Network Security

#### Properties

- [Documentation](https://www.checkpoint.com/cloudguard/cloud-network-security/)
- [Postman Collection](collections/cloudguard.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/cloudguard.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

## Common Properties

- [Website](https://www.checkpoint.com/cloudguard/)
- [Documentation](https://docs.cgn.portal.checkpoint.com/)
- [Developer  Portal](https://docs.cgn.portal.checkpoint.com/reference)
- [Getting Started](https://sc1.checkpoint.com/documents/CloudGuard_Dome9/Documentation/Getting-Started/Getting-started-with-CloudGuard.htm)
- [Authentication](https://sc1.checkpoint.com/documents/CloudGuard_Dome9/Documentation/API-Authentication.html)
- [Support](https://support.checkpoint.com/)
- [Community](https://community.checkpoint.com/)
- [Status Page](https://status.dome9.com/)
- [Privacy Policy](https://www.checkpoint.com/privacy/)
- [Terraform  Provider](https://registry.terraform.io/providers/dome9/dome9/latest/docs)
- [JSON-LD](json-ld/cloudguard-context.jsonld) — [JSON-LD](https://www.w3.org/TR/json-ld11/)
- [Spectral Rules](rules/cloudguard-rules.yml) — [Spectral](https://docs.stoplight.io/docs/spectral)

## Maintainers

**FN:** Kin Lane
**Email:** kin@apievangelist.com
