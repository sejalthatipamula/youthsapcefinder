# Host Data Models

[Host Workflow](host-workflow.md)

## Host object

```json
{
  "id": "host_001",
  "name": "Jordan Lee",
  "email": "jordan@example.com",
  "organizationName": "Maple Community Center"
}
```

A `Host` manages rental spaces. Each `Space` stores the host's `id` as `hostId`.

## Data used at each step

| Step | Data used | Data saved or updated |
| --- | --- | --- |
| List a space | Host ID, name, address, capacity, price, and rules | Create a `Space` with `hostId` |
| Set availability | Space ID, start time, end time, and open or blocked status | Save `Availability` with `spaceId` |
| Browse spaces | Listings, availability, and confirmed bookings | None |
| Request a space | Space ID, renter organization ID, start time, end time, event purpose, and attendee count | Create a `Booking` with status `Pending` |
| Review a request | Booking details, renter organization name, and the space's `hostId` | None |
| Approve a request | Pending booking, space's `hostId`, availability, and confirmed bookings | Set status to `Confirmed` if the host manages the space and the time is still open |
| Decline a request | Pending booking and the space's `hostId` | Set status to `Declined` if the host manages the space |

## Relationships

- One `Host` can manage multiple `Space` records.
- One `Space` can have multiple `Availability` and `Booking` records.
- Each `Booking` belongs to one `Space` and one `RenterOrganization`.
