# Host Data Models

[Host Workflow](host-workflow.md) · [All Data Models](data-models.md)

## Host object

```json
{
  "id": "host_001",
  "name": "Jordan Lee",
  "email": "jordan@example.com",
  "phone": "+1-425-555-0123",
  "organizationName": "Maple Community Center",
  "status": "Verified"
}
```

`status`: `PendingVerification` | `Verified` | `Suspended`

A `Host` manages spaces. Each `Space` stores the host's `id` as `hostId`.

## Space object

```json
{
  "id": "spc_001",
  "hostId": "host_001",
  "name": "Community Room B",
  "type": "LibraryRoom",
  "address": "15429 Bothell Everett Hwy, Mill Creek, WA",
  "capacity": 25,
  "price": { "amount": 0, "currency": "USD", "per": "hour" },
  "amenities": ["whiteboard", "wifi", "projector"],
  "rules": "No food. Adult must be present.",
  "accessibility": "Wheelchair accessible",
  "minNoticeHours": 72,
  "autoApprove": false,
  "status": "Live"
}
```

`type`: `LibraryRoom` | `ChurchHall` | `ParkShelter` | `CommunityCenter` | `Other`
`status`: `Draft` | `PendingApproval` | `Live` | `Hidden`

## Availability object

```json
{
  "id": "avl_001",
  "spaceId": "spc_001",
  "start": "2026-12-05T09:00:00-08:00",
  "end": "2026-12-05T20:00:00-08:00",
  "type": "Open",
  "recurrence": "WEEKLY;SA"
}
```

`type`: `Open` | `Blocked`

## Data used at each step

| Step | Data used | Data saved or updated |
| --- | --- | --- |
| List a space | Host ID, name, address, capacity, price, and rules | Create a `Space` with `hostId` and status `PendingApproval` |
| Set availability | Space ID, start time, end time, and open or blocked status | Save `Availability` with `spaceId` |
| Browse spaces | Listings, availability, and confirmed bookings | None |
| Request a space | Space ID, initiative ID, start time, end time, purpose, and attendee count | Create a `Booking` with status `PendingReview` |
| Reviewer approves | Booking and initiative | Set status to `PendingHost` |
| Review a request | Booking details, initiative name, adult on site, and the space's `hostId` | None |
| Approve a request | `PendingHost` booking, space's `hostId`, availability, and confirmed bookings | Set status to `Confirmed` if the host manages the space and the time is still open |
| Decline a request | `PendingHost` booking and the space's `hostId` | Set status to `Declined` if the host manages the space |

## Relationships

- One `Host` can manage multiple `Space` records.
- One `Space` can have multiple `Availability` and `Booking` records.
- Each `Booking` belongs to one `Space` and one `Initiative`.
