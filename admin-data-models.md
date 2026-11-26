# Admin Data Models

[Admin Workflow](admin-workflow.md) · [All Data Models](data-models.md)

## Admin

```json
{
  "id": "adm_001",
  "name": "Sejal T",
  "email": "admin@youthspacefinder.org",
  "role": "Admin",
  "mfaEnabled": true
}
```

`role`: `Admin` | `SuperAdmin` (only a SuperAdmin can add or remove admins)

## Case

```json
{
  "id": "case_001",
  "type": "ListingReport",
  "reason": "Listing photos don't match the space",
  "reportedBy": { "type": "Student", "id": "stu_001" },
  "linkedRecords": [{ "type": "Space", "id": "spc_001" }],
  "status": "InReview",
  "assignedAdminId": "adm_001",
  "openedAt": "2026-11-26T15:00:00Z"
}
```

`type`: `ListingReport` | `UserReport` | `BookingDispute` | `SafetyConcern` | `HostVerification` | `ReviewerVerification`
`status`: `Open` | `InReview` | `Resolved`

## AdminAction

```json
{
  "id": "act_001",
  "caseId": "case_001",
  "adminId": "adm_001",
  "action": "HideListing",
  "targetType": "Space",
  "targetId": "spc_001",
  "reason": "Misleading photos; host asked to update",
  "at": "2026-11-26T16:00:00Z"
}
```

`action`: `NoAction` | `VerifyHost` | `VerifyReviewer` | `HideListing` | `RestoreListing` | `CancelBooking` | `PauseAccount` | `SuspendAccount` | `ReinstateAccount`

## AuditEntry

Saved for every admin action and every status change made by any role. Audit entries can't be edited or deleted.

```json
{
  "id": "aud_001",
  "actor": { "type": "Admin", "id": "adm_001" },
  "event": "Space.status: Live -> Hidden",
  "caseId": "case_001",
  "at": "2026-11-26T16:00:00Z"
}
```

## Relationships

- One `Case` can link to many records (`Host`, `Space`, `Student`, `Initiative`, `Reviewer`, `Booking`).
- One `Case` can have many `AdminAction` records.
- Every `AdminAction` creates an `AuditEntry`.
