---
name: cloudguard-onboard-aws-account
description: Onboard an AWS account into Check Point CloudGuard, verify CloudGuard has the permissions it needs, and place the account in the right organizational unit.
api: CloudGuard Onboarding API
generated: '2026-09-05'
method: generated
source: openapi/cloudguard-onboarding-openapi.yml
base_url: https://api.dome9.com
operations:
  - AwsUnifiedOnboarding_GetStackConfig_post_/v2/AwsUnifiedOnboarding/StackConfig
  - AwsUnifiedOnboarding_Get_get_/v2/AwsUnifiedOnboarding/{id}
  - CloudAccounts_Post_post_/v2/CloudAccounts
  - CloudAccounts_Get_get_/v2/CloudAccounts
  - CloudAccounts_Get_get_/v2/CloudAccounts/{id}
  - CloudAccounts_GetMissingPermissionsAsync_get_/v2/cloudaccounts/{id}/MissingPermissions
  - CloudAccounts_SyncNow_post_/v2/cloudaccounts/{id}/SyncNow
  - CloudAccounts_PostAttachMulti_post_/v2/cloudaccounts/organizationalUnit/attach
  - CloudAccounts_Delete_delete_/v2/CloudAccounts/{id}
---

# Onboard an AWS account into CloudGuard

Authenticate every call with HTTP Basic: username is the CloudGuard **V2 API key id**, password is the
**API key secret** (portal → Settings → Credentials). The key inherits the permissions of the user that
created it — there are no API scopes.

```
curl -u $CG_KEY_ID:$CG_KEY_SECRET https://api.dome9.com/v2/CloudAccounts
```

Regional tenants use `https://api.{region}.dome9.com` (`eu1`, `ap1`, `ap2`, `ap3`, `cace1`) or, in the
Infinity Portal, `https://api.{region}.cgn.portal.checkpoint.com`. Pick the host that matches the tenant
before you start; the accounts in one region are not visible from another.

## Steps

1. **Check the account is not already onboarded.** `GET /v2/CloudAccounts`
   (`CloudAccounts_Get_get_/v2/CloudAccounts`) returns every AWS account in the tenant. Match on the AWS
   account number in `externalAccountNumber` before creating anything — this API has **no idempotency
   key**, so a repeated POST is a second onboarding attempt, not a no-op.
2. **Preferred: unified onboarding.** `POST /v2/AwsUnifiedOnboarding/StackConfig`
   (`AwsUnifiedOnboarding_GetStackConfig_post_/v2/AwsUnifiedOnboarding/StackConfig`) returns the
   configuration to hand to the AWS CloudFormation SDK to create the onboarding stack. Then poll
   `GET /v2/AwsUnifiedOnboarding/{id}` (`AwsUnifiedOnboarding_Get_get_/v2/AwsUnifiedOnboarding/{id}`)
   for onboarding state.
3. **Legacy path.** `POST /v2/CloudAccounts` (`CloudAccounts_Post_post_/v2/CloudAccounts`) with a
   `CloudAccountViewModel` body registers the account directly. Check Point's own operation description
   points at SK147832 for the manual permission grant this path requires. Returns **201**.
4. **Verify permissions.** `GET /v2/cloudaccounts/{id}/MissingPermissions`
   (`CloudAccounts_GetMissingPermissionsAsync_get_/v2/cloudaccounts/{id}/MissingPermissions`). A
   non-empty result means CloudGuard cannot fully read the account. Narrow it with
   `.../MissingPermissions/EntityType` and re-validate with
   `PUT /v2/cloudaccounts/{id}/MissingPermissions/Reset` after fixing the IAM role.
5. **Force a first fetch.** `POST /v2/cloudaccounts/{id}/SyncNow`
   (`CloudAccounts_SyncNow_post_/v2/cloudaccounts/{id}/SyncNow`) tells CloudGuard to pull the account's
   inventory immediately rather than waiting for the polling interval. Pair it with the
   `EntityFetchStatus` resource to watch the fetch complete.
6. **Place it in an organizational unit.** `POST /v2/cloudaccounts/organizationalUnit/attach`
   (`CloudAccounts_PostAttachMulti_post_/v2/cloudaccounts/organizationalUnit/attach`) attaches several
   accounts to one OU. Pass `null` as the target to mean the root OU.

## Rules

- **No idempotency.** Nothing on this API accepts an `Idempotency-Key`. Guard creates with the read in
  step 1 and never blind-retry a POST that timed out — read back first.
- **Deletion is one-way as far as the docs go.** `DELETE /v2/CloudAccounts/{id}` detaches the account;
  `DELETE /v2/cloudaccounts/{id}/DeleteForce` also removes every linked entity. Check Point publishes
  **no restore operation and no recovery window** for either. Treat both as irreversible and require
  human confirmation.
- **Errors are thin.** The published contract declares no 4xx responses. Expect
  `{"message":"..."}` with a 401 for a bad key, 403 when the generating user lacks the permission, and
  404 with `No HTTP resource was found that matches the request URI` for a wrong path. Paths are
  case-sensitive.
- **No rate limits are published** and no `RateLimit-*` headers are returned. Pace bulk onboarding
  conservatively and back off on any 5xx.
