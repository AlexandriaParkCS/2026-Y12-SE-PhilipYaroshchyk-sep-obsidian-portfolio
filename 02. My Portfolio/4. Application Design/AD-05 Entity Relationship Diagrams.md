
``` mermaid
--- 
title: YourCatsAndDogs Entity Relationship Diagram
config:
  er:
    useMaxWidth: true
--- 
erDiagram
    users ||--o{ pets : owns
    users |o--o{ bookings : sits
    users ||--o{ reviews : writes
    users ||--o{ reviews : receives
    users ||--o{ booking_requests : submits
    users ||--o{ messages : sends
    users ||--o{ messages : receives
    pets ||--o{ care_types : has
    pets ||--o{ bookings : "is subject of"
    bookings ||--o{ reviews : "is reviewed in"
    bookings ||--o{ booking_requests : receives

    users {
        INTEGER id PK
        TEXT username UK
        TEXT email UK
        INTEGER postcode
        TEXT photo
        TEXT about
        TEXT password_hash
    }
    pets {
        INTEGER id PK
        TEXT name
        TEXT species
        TEXT breed
        INTEGER yob
        INTEGER owner_id FK
    }
    care_types {
        INTEGER id PK
        TEXT name
        TEXT description
        TEXT schedule
        INTEGER pet_id FK
    }
    bookings {
        INTEGER id PK
        INTEGER pet_id FK
        INTEGER sitter_id FK
        TEXT start_date
        TEXT end_date
        INTEGER daily_price
    }
    reviews {
        INTEGER id PK
        INTEGER booking_id FK
        INTEGER reviewer_id FK
        INTEGER reviewee_id FK
        INTEGER score
        TEXT comment
    }
    booking_requests {
        INTEGER id PK
        INTEGER booking_id FK
        INTEGER sitter_id FK
    }
    messages {
        INTEGER id PK
        INTEGER sender_id FK
        INTEGER recipient_id FK
        TEXT body
        TIMESTAMP created_at
    }
```

**Cardinality details**

- `users ||--o{ pets` — every pet has exactly one owner (`pets.owner_id NOT NULL`); a user may own zero or more pets.
- `users |o--o{ bookings` — a booking has zero or one sitter (`bookings.sitter_id` is nullable until a sitter is confirmed); a user may sit for zero or more bookings.
- `pets ||--o{ bookings` — every booking is for exactly one pet; a pet may have zero or more bookings.
- `pets ||--o{ care_types` — every care type belongs to exactly one pet; a pet may have zero or more care types.
- `bookings ||--o{ booking_requests` — sitters apply for a booking via `booking_requests` (unique per booking/sitter pair); a booking may receive zero or more requests.
- `bookings ||--o{ reviews` — each review belongs to exactly one booking; a booking may accumulate zero or more reviews (in practice, up to two — one from each party, enforced by `UNIQUE (booking_id, reviewer_id)`).
- `users ||--o{ reviews` (writes/receives) — a review always has exactly one reviewer and one reviewee, both foreign keys into `users`.
- `users ||--o{ messages` (sends/receives) — every message has exactly one sender and one recipient, both foreign keys into `users`.
