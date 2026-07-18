***Register / Login***

This process is the entry point to the application, allowing a new pet owner or sitter to create an account or existing users to authenticate before accessing their pets, bookings and messages.

Summary of user registration:

``` mermaid
--- 
title: Register
config:
  flowchart:
    useMaxWidth: true
--- 
flowchart TD
    subgraph Input
        I1[Username]
        I2[Email address]
        I3[Password]
    end
    subgraph Process
        P0{"Username, email & <br/>password all provided?"}
        P1[Hash password <br/>Werkzeug scrypt]
        P2[INSERT into users]
        P3{Insert succeeded?}
    end
    subgraph Output
        O1[Redirect to login page]
        O2["Flashed error message <br/>(required / already registered)"]
    end
    Input --> P0
    P0 -->|No| O2
    P0 -->|Yes| P1 --> P2 --> P3
    P3 -->|Yes| O1
    P3 -->|No, duplicate <br/>username/email| O2
```

Summary of user login:

``` mermaid
--- 
title: Login
config:
  flowchart:
    useMaxWidth: true
--- 
flowchart TD
    subgraph Input
        I1[Username]
        I2[Password]
    end
    subgraph Process
        P1{User found <br/>by username?}
        P2{Password hash <br/>matches stored hash?}
        P3[Clear session, store <br/>user id in new session]
    end
    subgraph Output
        O1[Active session, <br/>redirect to home page]
        O2["Flashed error <br/>(Incorrect username)"]
        O3["Flashed error <br/>(Incorrect password)"]
    end
    Input --> P1
    P1 -->|No| O2
    P1 -->|Yes| P2
    P2 -->|No| O3
    P2 -->|Yes| P3 --> O1
```

<hr>

***List a Pet***

This process lets a pet owner register a pet on the platform and describe the ongoing care it needs, so that the pet can later be booked in for sitting.

``` mermaid
--- 
title: Add a Pet
config:
  flowchart:
    useMaxWidth: true
--- 
flowchart TD
    subgraph Input
        I1[Name]
        I2[Species]
        I3[Breed]
        I4[Year of birth]
    end
    subgraph Process
        P1{All fields provided?}
        P2["INSERT into pets <br/>(owner_id = current user)"]
    end
    subgraph Output
        O1[Pet listed on <br/>owner's home page]
        O2[Flashed error message]
    end
    Input --> P1
    P1 -->|No| O2
    P1 -->|Yes| P2 --> O1
```

Summary of adding a care type for a pet:

``` mermaid
--- 
title: Add Care Details
config:
  flowchart:
    useMaxWidth: true
--- 
flowchart TD
    subgraph Input
        I1[Pet]
        I2[Care type name]
        I3[Description]
        I4[Schedule]
    end
    subgraph Process
        P1["Flash error for any <br/>missing field (insert still <br/>proceeds regardless)"]
        P2[INSERT into care_types]
    end
    subgraph Output
        O1[Care type shown on <br/>pet detail page]
        O2[Flashed error message, <br/>if a field was missing]
    end
    Input --> P1 --> P2 --> O1
    P1 -.-> O2
```

<hr>

***Book a Sitting***

This process covers the full lifecycle of a booking: a pet owner opens a sitting window for a pet, sitters apply to look after it, and the owner confirms one applicant.

Summary of creating a booking (pet owner):

``` mermaid
--- 
title: Create a Booking
config:
  flowchart:
    useMaxWidth: true
--- 
flowchart TD
    subgraph Input
        I1[Pet]
        I2[Start date]
        I3[End date]
        I4[Daily price]
    end
    subgraph Process
        P1{Pet belongs to <br/>logged-in user?}
        P2{"Dates & price valid, <br/>not in the past, <br/>end date ≥ start date?"}
        P3[Round daily price]
        P4["INSERT into bookings <br/>(sitter_id left unset)"]
    end
    subgraph Output
        O1[Unconfirmed booking <br/>shown on pet detail page]
        O2[Flashed error, <br/>redirected to home]
        O3[Flashed validation error]
    end
    Input --> P1
    P1 -->|No| O2
    P1 -->|Yes| P2
    P2 -->|No| O3
    P2 -->|Yes| P3 --> P4 --> O1
```

Summary of applying for a booking (sitter):

``` mermaid
--- 
title: Apply for a Booking
config:
  flowchart:
    useMaxWidth: true
--- 
flowchart TD
    subgraph Input
        I1[Booking to apply for]
    end
    subgraph Process
        P1{"Profile complete? <br/>(photo, postcode, about)"}
        P2{Booking exists with <br/>no confirmed sitter?}
        P3[INSERT into booking_requests]
    end
    subgraph Output
        O1[Applicant added to <br/>booking's request list]
        O2["Flashed error <br/>(incomplete profile)"]
        O3["Flashed error <br/>(not found / confirmed)"]
    end
    Input --> P1
    P1 -->|No| O2
    P1 -->|Yes| P2
    P2 -->|No| O3
    P2 -->|Yes| P3 --> O1
```

Summary of confirming a booking (pet owner):

``` mermaid
--- 
title: Confirm a Booking
config:
  flowchart:
    useMaxWidth: true
--- 
flowchart TD
    subgraph Input
        I1[Booking request to accept]
    end
    subgraph Process
        P1{Request belongs to a <br/>booking on the owner's pet?}
        P2[UPDATE bookings, <br/>set sitter_id]
    end
    subgraph Output
        O1[Booking confirmed, added <br/>to sitter's list of sittings]
        O2["Flashed error <br/>(not found / no permission)"]
    end
    Input --> P1
    P1 -->|No| O2
    P1 -->|Yes| P2 --> O1
```

<hr>

***Leave a Review***

This process lets either party in a completed booking rate and comment on the other, building trust for future bookings.

``` mermaid
--- 
title: Leave a Review
config:
  flowchart:
    useMaxWidth: true
--- 
flowchart TD
    subgraph Input
        I1[Booking]
        I2[Reviewee]
        I3[Score 1-5]
        I4[Comment]
    end
    subgraph Process
        P1{"Booking confirmed & reviewer <br/>is owner or sitter for it?"}
        P2[INSERT into reviews]
        P3{"Reviewer already <br/>reviewed this booking? <br/>(UNIQUE constraint)"}
    end
    subgraph Output
        O1[Review recorded, visible on <br/>reviewee's profile & average score]
        O2["Flashed 'not eligible' error"]
        O3[Flashed database error]
    end
    Input --> P1
    P1 -->|No| O2
    P1 -->|Yes| P2 --> P3
    P3 -->|No| O1
    P3 -->|Yes| O3
```

<hr>

***Search***

This process lets pet owners find a suitable sitter, and sitters find pets nearby that need care.

Summary of searching for a sitter:

``` mermaid
--- 
title: Search for a Sitter
config:
  flowchart:
    useMaxWidth: true
--- 
flowchart TD
    subgraph Input
        I1[Search query]
    end
    subgraph Process
        P1{Query provided?}
        P2[Trim query]
        P3["Match against username, <br/>postcode, about (LIKE)"]
        P4[Join average review <br/>score & review count]
    end
    subgraph Output
        O1[List of matching sitters, <br/>with rating]
        O2[Empty results page]
    end
    Input --> P1
    P1 -->|No| O2
    P1 -->|Yes| P2 --> P3 --> P4 --> O1
```

Summary of searching for pets needing care:

``` mermaid
--- 
title: Search for Pets
config:
  flowchart:
    useMaxWidth: true
--- 
flowchart TD
    subgraph Input
        I1[Free-text query]
        I2[Min daily price]
        I3[Max daily price]
    end
    subgraph Process
        P1{Query provided?}
        P2["Match against pet name, <br/>species, breed (LIKE)"]
        P3[Exclude own pets & bookings <br/>with a confirmed sitter]
        P4["Apply optional min/max <br/>price filters"]
    end
    subgraph Output
        O1[List of matching pets <br/>and their open bookings]
        O2[Empty results page]
    end
    Input --> P1
    P1 -->|No| O2
    P1 -->|Yes| P2 --> P3 --> P4 --> O1
```

<hr>

***Send a Message***

This process lets a pet owner and sitter communicate directly about a pet or booking.

``` mermaid
--- 
title: Send a Message
config:
  flowchart:
    useMaxWidth: true
--- 
flowchart TD
    subgraph Input
        I1[Recipient]
        I2[Message body]
    end
    subgraph Process
        P1{Recipient exists & <br/>is not the sender?}
        P2{Message body <br/>non-empty?}
        P3[INSERT into messages <br/>with current timestamp]
    end
    subgraph Output
        O1[Message appended to thread, <br/>inbox preview updated]
        O2[404 Not Found]
        O3["Flashed 'cannot be empty' error"]
    end
    Input --> P1
    P1 -->|No| O2
    P1 -->|Yes| P2
    P2 -->|No| O3
    P2 -->|Yes| P3 --> O1
```
