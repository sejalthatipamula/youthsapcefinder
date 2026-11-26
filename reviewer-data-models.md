# Reviewer Data Models

[Reviewer Workflow](reviewer-workflow.md) · [All Data Models](data-models.md)

## Reviewer

```json
{
  "id": "rev_001",
  "name": "Anil Rao",
  "email": "arao@school.edu",
  "phone": "+1-425-555-0111",
  "role": "Teacher",
  "affiliation": "Jackson High School",
  "status": "Verified",
  "verifiedByAdminId": "adm_001",
  "maxActiveInitiatives": 10
}
```

`status`: `PendingVerification` | `Verified` | `Suspended`

## ReviewDecision

```json
{
  "id": "rd_001",
  "reviewerId": "rev_001",
  "targetType": "Booking",
  "targetId": "bkg_001",
  "decision": "Approved",
  "reason": "Supervised by me on site",
  "at": "2026-11-26T18:00:00Z"
}
```

`targetType`: `Initiative` | `Booking`
`decision`: `Approved` | `ChangesRequested` | `Rejected` | `Declined`

## StandingApproval

Lets repeat sessions skip reviewer review.

```json
{
  "id": "sa_001",
  "reviewerId": "rev_001",
  "initiativeId": "ini_001",
  "spaceId": "spc_001",
  "pattern": "WEEKLY;TU;16:00-18:00",
  "validUntil": "2027-06-15",
  "active": true
}
```

## Relationships

- One `Reviewer` can sponsor many `Initiative` records.
- Each `ReviewDecision` belongs to one `Reviewer` and points to one `Initiative` or `Booking`.
- One `Initiative` can have several `StandingApproval` records.
