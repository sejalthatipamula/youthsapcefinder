# Student Data Models

[Student Workflow](student-workflow.md) · [All Data Models](data-models.md)

## Student

```json
{
  "id": "stu_001",
  "firstName": "Aria",
  "lastName": "Patel",
  "email": "aria@example.com",
  "dateOfBirth": "2011-04-12",
  "school": "Jackson High School",
  "grade": 10,
  "zip": "98012",
  "status": "Active",
  "noShowCount": 0,
  "createdAt": "2026-11-26T10:00:00Z"
}
```

`status`: `PendingGuardian` | `Active` | `Paused` | `Suspended`

## GuardianConsent

```json
{
  "id": "gc_001",
  "studentId": "stu_001",
  "guardianName": "Priya Patel",
  "guardianEmail": "priya@example.com",
  "guardianPhone": "+1-425-555-0100",
  "status": "Approved",
  "approvedAt": "2026-11-26T12:00:00Z"
}
```

`status`: `Pending` | `Approved` | `Revoked`

## Initiative

The student group that books spaces. It replaces `RenterOrganization` in the host docs.

```json
{
  "id": "ini_001",
  "title": "Mill Creek Math Circle",
  "description": "Weekly peer tutoring for middle schoolers",
  "category": "Study",
  "leadStudentId": "stu_001",
  "coLeadStudentIds": ["stu_002"],
  "reviewerId": "rev_001",
  "expectedGroupSize": 15,
  "ageRange": "11-14",
  "status": "Approved"
}
```

`status`: `PendingReview` | `Approved` | `ChangesRequested` | `Rejected` | `Archived`

## Booking (student-facing fields)

```json
{
  "id": "bkg_001",
  "spaceId": "spc_001",
  "initiativeId": "ini_001",
  "requestedByStudentId": "stu_001",
  "start": "2026-12-05T16:00:00-08:00",
  "end": "2026-12-05T18:00:00-08:00",
  "purpose": "Math tutoring session",
  "attendeeCount": 12,
  "adultOnSite": { "name": "Mr. Rao", "phone": "+1-425-555-0111" },
  "equipment": ["whiteboard"],
  "status": "PendingReview",
  "statusHistory": [
    { "status": "PendingReview", "by": "stu_001", "at": "2026-11-26T14:00:00Z" }
  ]
}
```

## CheckIn and Review

```json
{ "id": "chk_001", "bookingId": "bkg_001", "studentId": "stu_001", "at": "2026-12-05T16:02:00-08:00" }
```

```json
{ "id": "rvw_001", "bookingId": "bkg_001", "spaceId": "spc_001", "rating": 5, "comment": "Quiet and clean" }
```

## Relationships

- One `Student` can lead or co-lead several `Initiative` records.
- Each `Initiative` has one `Reviewer`.
- One `Initiative` can have many `Booking` records.
- Each `Booking` can have one `CheckIn` and one `Review`.
