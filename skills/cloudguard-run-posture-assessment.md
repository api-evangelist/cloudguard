---
name: cloudguard-run-posture-assessment
description: Run a CloudGuard compliance ruleset against a cloud account, read the assessment result, and pull the executive report.
api: CloudGuard Posture Management API
generated: '2026-09-05'
method: generated
source: openapi/cloudguard-posture-management-openapi.yml
base_url: https://api.dome9.com
operations:
  - Assessment_RunBundleV2Async_post_/v2/assessment/bundleV2
  - AssessmentHistoryV2_GetLastAssessmentResults_post_/v2/AssessmentHistoryV2/LastAssessmentResults
  - AssessmentHistoryV2_GetBundleResults_get_/v2/AssessmentHistoryV2/bundleResults
  - AssessmentHistoryV2_GetHistoryAsync_get_/v2/AssessmentHistoryV2/{id}
  - AssessmentHistoryV2_GetAssessmentResultCsv_get_/v2/AssessmentHistoryV2/csv/{assessmentResultId}
  - AssessmentHistoryV2_GetAssessmentExecutiveReportCSV_get_/v2/AssessmentHistoryV2/{assessmentId}/ExecutiveReport/csv
  - AssessmentHistoryV2_GetAssessmentTrendV2_get_/v2/AssessmentHistoryV2/assessmentTrendV2
  - ContinuousCompliancePolicyV2_Post_post_/v2/ContinuousCompliancePolicyV2
---

# Run a posture assessment

HTTP Basic with the V2 API key id / secret, base `https://api.dome9.com/v2/`.

## One-off assessment

1. **Run a ruleset.** `POST /v2/assessment/bundleV2`
   (`Assessment_RunBundleV2Async_post_/v2/assessment/bundleV2`). The body names the ruleset (bundle) and
   the target cloud account. CloudGuard maintains rulesets that implement CIS, PCI DSS, HIPAA, GDPR,
   NIST and ISO control sets; the rules themselves are written in GSL and browsable at
   <https://gsl.dome9.com/>.
2. **Read the result.** `GET /v2/AssessmentHistoryV2/{id}`
   (`AssessmentHistoryV2_GetHistoryAsync_get_/v2/AssessmentHistoryV2/{id}`) for one run, or
   `POST /v2/AssessmentHistoryV2/LastAssessmentResults` for the latest per target. Use
   `.../LastAssessmentResults/minimized` when you only need pass/fail counts — the full result set is
   large and **this API publishes no pagination at all**, so a broad query returns everything in one
   response.
3. **Export.** `GET /v2/AssessmentHistoryV2/csv/{assessmentResultId}` and
   `GET /v2/AssessmentHistoryV2/{assessmentId}/ExecutiveReport/csv` return
   `application/octet-stream`, not JSON.
4. **Trend.** `GET /v2/AssessmentHistoryV2/assessmentTrendV2` and
   `.../assessmentTrendOrganizationalUnit` give the posture trend over time; use
   `startTimestamp`/`endTimestamp` to bound the window.

## Continuous assessment

`POST /v2/ContinuousCompliancePolicyV2` binds a ruleset to a target so CloudGuard evaluates it
continuously and emits findings. Validate ruleset versions first with
`POST /v2/ContinuousCompliancePolicyV2/EvaluateRulesetVersions`.

## Rules

- **Unbounded result sets.** No `page`, `limit`, `offset` or cursor parameter exists on any operation.
  Scope by cloud account, organizational unit, ruleset or time range in the request body instead, and
  never assume a response is small.
- **Policies have no rollback.** Updating a continuous compliance policy is `PUT`, and removing one is
  `DELETE /v2/ContinuousCompliancePolicyV2/{id}`. There is no version history and no restore. Read the
  current policy before you change it and keep the previous body yourself.
- **`DELETE /v2/AssessmentHistoryV2` deletes assessment history.** No published recovery window.
  Human confirmation before calling it.
- No idempotency keys, no published rate limits, no 4xx documented in the contract.
