***Pet Sitting Management***

The following UML class diagram for YourCatsAndDogs models the key objects and their relationships that support pet owners listing pets and care needs, pet sitters requesting and confirming bookings, and both parties messaging each other and reviewing each other's services.


``` mermaid
--- 
title: YourCatsAndDogs Class Diagram
config:
  class:
    useMaxWidth: true
--- 
classDiagram
    direction TB
    class User {
        +int id
        +string username
        +string email
        +int postcode
        +string photo
        +string about
        -string password_hash
        +register()
        +login()
        +logout()
        +updateProfile()
        +uploadPhoto()
    }
    class Pet {
        +int id
        +string name
        +string species
        +string breed
        +int yob
        +addCareType()
        +getDetails()
    }
    class CareType {
        +int id
        +string name
        +string description
        +string schedule
    }
    class Booking {
        +int id
        +date start_date
        +date end_date
        +int daily_price
        +requestSitter(user)
        +confirm(sitter)
    }
    class BookingRequest {
        +int id
        +accept()
    }
    class Review {
        +int id
        +int score
        +string comment
        +submit()
    }
    class Message {
        +int id
        +string body
        +datetime created_at
        +send()
    }

    User "1" --> "0..*" Pet : owns
    Pet "1" --> "0..*" CareType : requires
    Pet "1" --> "0..*" Booking : "is subject of"
    User "0..1" --> "0..*" Booking : sits
    Booking "1" --> "0..*" BookingRequest : receives
    User "1" --> "0..*" BookingRequest : submits
    Booking "1" --> "0..*" Review : "is reviewed in"
    User "1" --> "0..*" Review : writes
    User "1" --> "0..*" Review : receives
    User "1" --> "0..*" Message : sends
    User "1" --> "0..*" Message : receives
```

The `User` class represents both pet owners and sitters — there is no separate role subclass, since a single account can list pets *and* apply to sit for others. Each `User` can own multiple `Pet`s, and each `Pet` can have multiple `CareType` requirements describing how it should be looked after. A `Pet` can be booked in for sitting via a `Booking`, which starts without a confirmed sitter: interested users submit a `BookingRequest`, and the owner's `confirm()` call assigns one request's sitter to the booking. Once a `Booking` has taken place, either party can `submit()` a `Review` of the other, and users can `send()` `Message`s to each other independently of any booking.
