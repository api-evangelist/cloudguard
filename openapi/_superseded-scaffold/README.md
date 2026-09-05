# Superseded scaffold specifications

These files were authored by the API Evangelist pipeline as a *best-effort* description of the
CloudGuard API (they say so themselves: `info.description` begins "Best-effort OpenAPI 3.1
description..."). They were **not** published by Check Point.

On 2026-09-05 the enrichment pipeline located the provider's own OpenAPI documents, embedded in
the CloudGuard Developer Hub reference pages at https://docs.cgn.portal.checkpoint.com/reference —
23 first-party definitions covering 823 operations. Those are now in `openapi/` and the raw
harvested JSON is in `openapi/_original/`.

These scaffolds are retained only for audit of what the catalog previously held. They are not
referenced from `apis.yml` and must not be scored, derived from, or republished.
