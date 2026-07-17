# Booking Systems Integration

Elementeer integrates with WordPress booking and scheduling plugins — Amelia, Simply Schedule Appointments, and The Events Calendar. Your AI agent can detect active booking systems, read bookings, and manage appointments.

## Supported Plugins

| Plugin | Detection | Capabilities |
|--------|-----------|-------------|
| **Amelia** | wpamelia | Bookings, appointments, services, employees, customers, stats |
| **Simply Schedule Appointments** | ssa | Appointments, appointment types, availability |
| **The Events Calendar** | tribe-events | Events, venues, organizers, tickets |

## Amelia Integration

Amelia is a full-featured booking plugin for service-based businesses. Elementeer detects it automatically:

```
Check if Amelia is installed and show booking stats for this month.
```

### Detection and Status

```json
{
  "amelia": {
    "active": true,
    "version": "7.8",
    "services": 12,
    "employees": 5,
    "bookings_this_month": 47,
    "revenue_this_month": "3,250.00"
  }
}
```

### Services

```
List all Amelia services with durations and prices.
```

```json
{
  "services": [
    {
      "id": 1,
      "name": "Consultation (60 min)",
      "duration": 3600,
      "price": 150.00,
      "category": "Consulting"
    },
    {
      "id": 2,
      "name": "Follow-up (30 min)",
      "duration": 1800,
      "price": 75.00,
      "category": "Consulting"
    }
  ]
}
```

### Bookings

```
Show all upcoming bookings for this week.
```

```json
{
  "bookings": [
    {
      "id": 482,
      "customer": "Jane Smith",
      "service": "Consultation (60 min)",
      "employee": "Dr. Miller",
      "datetime": "2026-07-20T10:00:00Z",
      "status": "approved",
      "price": 150.00
    }
  ],
  "total_upcoming": 12
}
```

### Customer Management

```
Find bookings for customer email jane@example.com.
```

### Stats and Reports

```
What are the most booked services this quarter?
```

```
Show employee utilization rates for July.
```

## Simply Schedule Appointments

### Availability

```
Show available appointment slots for next Tuesday.
```

### Appointment Types

```
List all appointment types with their durations.
```

## The Events Calendar

### Events

```
List upcoming events for the next 30 days.
```

```json
{
  "events": [
    {
      "id": 87,
      "title": "Summer Workshop 2026",
      "start_date": "2026-08-15T09:00:00",
      "end_date": "2026-08-15T17:00:00",
      "venue": "Conference Center",
      "organizer": "Acme Events Team",
      "tickets_available": 45
    }
  ],
  "total_upcoming": 8
}
```

### Venues and Organizers

```
List all event venues with addresses.
```

```
Show events organized by "Acme Events Team".
```

### Tickets

```
How many tickets have been sold for the Summer Workshop?
```

```
Update the ticket price for the "Early Bird" ticket to $149.
```

## Availability Checks

The agent can check availability across booking systems:

```
Is there an available consultation slot this Thursday afternoon?
```

The agent queries the booking system for open slots matching the criteria and returns available times.

## Booking Integration Architecture

Elementeer's booking integrations follow a common pattern:

1. **Detection** — auto-discovery of active booking plugins on site activation
2. **Schema Mapping** — each plugin's data structures are mapped to typed Elementeer tools
3. **Unified Interface** — the agent uses consistent patterns regardless of which plugin is active
4. **Plugin-Native Writes** — all write operations go through the booking plugin's native API, respecting hooks and validation

!!! info "Pro tier features"
    Advanced booking operations — creating appointments, managing employee schedules,
    and running detailed reports — require the `@elementeer/pro` addon with the
    `booking:write` capability.
