---
name: cloudguard-configure-compliance-notifications
description: Wire CloudGuard continuous-compliance findings out to a webhook, SNS, Slack, Teams, a ticketing system or a cloud security hub, and check delivery health.
api: CloudGuard Administration API
generated: '2026-09-05'
method: generated
source: openapi/cloudguard-administration-openapi.yml
base_url: https://api.dome9.com
operations:
  - ContinuousComplianceNotification_Get_get_/v2/Compliance/ContinuousComplianceNotification
  - ContinuousComplianceNotification_GetByName_get_/v2/Compliance/ContinuousComplianceNotification/get-by-name
  - ContinuousComplianceNotification_Post_post_/v2/Compliance/ContinuousComplianceNotification
  - ContinuousComplianceNotification_Put_put_/v2/Compliance/ContinuousComplianceNotification/{id}
  - ContinuousComplianceNotification_Delete_delete_/v2/Compliance/ContinuousComplianceNotification/{id}
  - ContinuousComplianceNotification_PublishOpenedFindingsByPolicyIdAsync_post_/v2/Compliance/ContinuousComplianceNotification/PublishOpenedFindings/{id}
  - ContinuousComplianceNotification_GetAllCircuitBreakerAsync_get_/v2/Compliance/ContinuousComplianceNotification/CircuitBreaker
  - ContinuousComplianceNotification_DeleteCircuitBreakerAsync_delete_/v2/Compliance/ContinuousComplianceNotification/CircuitBreaker/{id}/{integrationType}
  - Integration_GetAllIntegrations_get_/v2/integration
  - Integration_CreateIntegration_post_/v2/integration
---

# Route CloudGuard findings to an external system

HTTP Basic with the V2 API key id / secret, base `https://api.dome9.com/v2/`.

## Steps

1. **List what already exists.** `GET /v2/Compliance/ContinuousComplianceNotification` and
   `GET /v2/integration`. Check by name with
   `GET /v2/Compliance/ContinuousComplianceNotification/get-by-name` before creating — duplicates are
   easy to make and there is no idempotency key.
2. **Create the delivery target.** `POST /v2/integration`
   (`Integration_CreateIntegration_post_/v2/integration`) takes `{name, type, configuration}`.
3. **Create the notification.** `POST /v2/Compliance/ContinuousComplianceNotification` with a
   `ContinuousComplianceNotificationPostViewModel`:
   - `changeDetection` selects the channels — `webhookIntegrationState`, `snsSendingState`,
     `slackIntegrationState`, `teamsIntegrationState`, `eventarcIntegrationState`,
     `awsSecurityHubIntegrationState`, `azureSecurityCenterIntegrationState`,
     `externalTicketCreatingState`, `emailSendingState`, `emailPerFindingSendingState`.
   - the matching `*Data` block carries the target. For a webhook that is
     `WebhookNotificationDataViewModel`: `url`, `httpMethod`, `authMethod`, `username`, `password`,
     `formatType`, `payloadFormat`, `ignoreCertificate`, `advancedUrl`.
   - `filter` scopes it: `severities`, `entityTypes`, `entityTags`, `entityNames`, `entityIds`.
   - `scheduledReport` with a `cronExpression` gives a periodic report instead of live change
     detection.
4. **Backfill.** `POST /v2/Compliance/ContinuousComplianceNotification/PublishOpenedFindings/{id}`
   replays currently-open findings through the target — use it once after wiring, not on a schedule.
5. **Watch delivery health.** `GET /v2/Compliance/ContinuousComplianceNotification/CircuitBreaker`
   lists tripped targets. Reset one with
   `DELETE /v2/Compliance/ContinuousComplianceNotification/CircuitBreaker/{id}/{integrationType}`.

## Rules

- **CloudGuard publishes no webhook payload schema.** `formatType` and `payloadFormat` are selectable,
  but no document describes what CloudGuard POSTs for any of them. Do not promise a receiver shape you
  have not observed. The only published model, `WebhookResponseMessage {requestTime, responseContent}`,
  describes what CloudGuard records about *your* response.
- **No delivery signing.** There is no HMAC header, timestamp or replay protection. Authentication of
  the delivery is only what you configure in `authMethod` / `username` / `password`. Never set
  `ignoreCertificate` to true for a production endpoint.
- **Credentials go in the request body.** `TicketingSystemNotificationDataViewModel` carries `user` and
  `pass` in clear JSON. Treat any GET of a notification as returning secrets and do not log it.
- **`DELETE` of a notification is not reversible** and there is no published recovery window. Read it
  back and keep the body before deleting.
- No retry/backoff policy is published beyond the existence of the circuit breaker.
