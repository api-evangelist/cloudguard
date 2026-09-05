---
name: cloudguard-triage-findings
description: Search, acknowledge, comment on, re-prioritise, assign, archive and re-open CloudGuard compliance findings safely.
api: CloudGuard Events API
generated: '2026-09-05'
method: generated
source: openapi/cloudguard-events-openapi.yml
base_url: https://api.dome9.com
operations:
  - Finding_Search_post_/v2/Compliance/Finding/search
  - Finding_SearchAggregate_post_/v2/Compliance/Finding/searchAggregate
  - Finding_GetFinding_get_/v2/Compliance/Finding/{id}
  - Finding_GetStatsByProperty_get_/v2/Compliance/Finding/stats/aggregatedbyproperty
  - Finding_Acknowledge_put_/v2/Compliance/Finding/{id}/acknowledge
  - Finding_BulkAcknowledge_put_/v2/Compliance/Finding/bulk/acknowledge
  - Finding_Assign_put_/v2/Compliance/Finding/{id}/assign
  - Finding_ChangeSeverity_put_/v2/Compliance/Finding/{id}/severity
  - Finding_AddComment_post_/v2/Compliance/Finding/{id}/comment
  - Finding_Archive_post_/v2/Compliance/Finding/{id}/archive
  - Finding_Archive_post_/v2/Compliance/Finding/{id}/unarchive
  - Finding_BulkArchive_put_/v2/Compliance/Finding/bulk/archive
  - Finding_BulkArchive_put_/v2/Compliance/Finding/bulk/unarchive
  - Finding_SelectAllClose_post_/v2/Compliance/Finding/selectAll/archive/close
  - Finding_BulkDeleteAsync_post_/v2/Compliance/Finding/bulk/close
  - ExternalFindings_Search_post_/v2/ExternalFindings/search
  - ExternalFindings_Post_post_/v2/ExternalFindings
---

# Triage CloudGuard findings

HTTP Basic with the V2 API key id / secret, base `https://api.dome9.com/v2/`.

## Read first

- `POST /v2/Compliance/Finding/search` — the primary query surface. Filter by severity, entity type,
  tags, names, ids and time range in the body.
- `POST /v2/Compliance/Finding/searchAggregate` and
  `GET /v2/Compliance/Finding/stats/aggregatedbyproperty` — counts without pulling every row. Prefer
  these for reporting; there is **no pagination on this API**, so an unbounded search returns the whole
  result set.
- `GET /v2/Compliance/Finding/{id}` for one finding. `POST /v2/Compliance/Finding/getByKey` when you
  hold the finding key rather than the id.
- `GET /v2/Compliance/Finding/Sources` and `/origins` enumerate what can produce a finding — useful
  before you filter on either.

## Non-destructive actions — safe for an agent

| Intent | Single | Bulk |
|---|---|---|
| Mark reviewed | `PUT /{id}/acknowledge` | `PUT /bulk/acknowledge`, `PUT /selectAll/acknowledge` |
| Route to an owner | `PUT /{id}/assign` | `PUT /bulk/assign`, `PUT /selectAll/assign` |
| Re-prioritise | `PUT /{id}/severity` | `PUT /bulk/severity`, `PUT /selectAll/severity` |
| Add context | `POST /{id}/comment` | `PUT /bulk/comment`, `PUT /selectAll/comment` |

## Reversible action

`POST /v2/Compliance/Finding/{id}/archive` hides a finding; **`POST /v2/Compliance/Finding/{id}/unarchive`
brings it back**, and the bulk pair `PUT /bulk/archive` / `PUT /bulk/unarchive` mirrors it. This is the
one write on the findings surface with a documented reversal. Check Point publishes **no time window**
for the reversal, so do not tell a user "you have N days" — you do not know that.

## Destructive actions — require explicit human approval

- `POST /v2/Compliance/Finding/bulk/close` and `/selectAll/close` — closes findings.
- `POST /v2/Compliance/Finding/selectAll/archive/close` — archives **and** closes everything matching a
  filter. `selectAll` operates on the whole filtered set, not a supplied list of ids; a wrong filter is
  an unbounded blast radius.
- `DELETE /v2/Compliance/Finding/{id}` and `DELETE /v2/Compliance/Finding/archive/{id}` — deletion. No
  undelete is published.
- `DELETE /v2/ExternalFindings` — deletes external findings in bulk.

Always run the equivalent `search` with the same filter first, show the count, and get confirmation
before any `selectAll` or `DELETE` call.

## Rules

- **No idempotency key.** A retried bulk close is a second bulk close. Read back with `search` instead
  of retrying blind.
- **Errors are not in the contract.** 401 `{"message":"Authorization has been denied for this request."}`
  for a bad key; 403 when the key's user lacks the permission; 404 for a wrong (case-sensitive) path.
- Pushing findings **in**: `POST /v2/ExternalFindings` accepts third-party findings into the same
  triage surface, and `POST /v2/ExternalFindings/{id}/Archive` archives them.
