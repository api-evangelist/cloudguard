# CloudGuard (cloudguard)

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **Not from the company, and here with a question?** You are welcome here — we would rather be the
> front line and point you the right way than have a good report go nowhere. What this repository
> can answer is narrow, though, so it is worth knowing who you are actually looking for:
>
> - **A question about how the API works, an account, billing, or a bug in the service** — that is
>   the company's own support, not us. We profile this API; we do not operate it and cannot see
>   your account.
> - **A bug in an open-source project we only catalog** — file it on that project's own repository.
>   This has happened with a real and correct bug report that reached us instead of the people who
>   could fix it, which helped nobody.
> - **Anything about this listing itself** — the description, the tags, the rating, a missing or
>   wrong artifact — is ours. Open an issue here.
> - **Not sure, or something general about API Evangelist or APIs.io** — open an issue on the
>   [APIs.io Inbox](https://github.com/api-search/inbox) and we will route it.
>
> **This repository contains no software, and we will never ask you to download anything.** There is
> no build, release, installer, or binary here — only text and machine-readable API descriptions, so
> there is nothing here that can be "corrupt" or need "repairing". Any issue, comment, or email
> claiming otherwise and offering a download link is not from us and is hostile. Do not follow the
> link; it is a lure. Report it to GitHub and, if you like, tell us at
> [info@apievangelist.com](mailto:info@apievangelist.com) so we can take it down.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

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
