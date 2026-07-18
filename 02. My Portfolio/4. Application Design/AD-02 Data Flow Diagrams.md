***Context Diagram (Level 0)***

The application interacts with two human actors and one data store, shown below.

``` mermaid
--- 
title: YourCatsAndDogs Context Diagram (Level 0)
config:
  flowchart:
    useMaxWidth: true
--- 
flowchart TD
    PO[Pet Owner]
    PS[Pet Sitter]
    SYS((0<br/>YourCatsAndDogs))
    DB[(SQLite Database)]

    PO -->|register, login, add pets & <br/>care needs, create bookings, <br/>confirm sitters, message, review| SYS
    SYS -->|account & booking status, <br/>applicants, messages, <br/>confirmations & errors| PO
    PS -->|register, login, search, <br/>apply for bookings, message, review| SYS
    SYS -->|account & booking status, <br/>search results, messages, <br/>confirmations & errors| PS
    SYS -->|new & updated records| DB
    DB -->|stored records| SYS
```

The actors include:
- **Pet Owner**: a user who lists pets and their care needs, opens sitting bookings, reviews applicants and confirms a sitter, messages sitters, and leaves reviews after a sitting.
- **Pet Sitter**: a user who searches for pets needing care, applies for open bookings, messages owners, and leaves reviews after a sitting.
- **Database**: a SQLite database (see `flaskr/db.py`) that persists every record the system creates — users, pets, care types, bookings, booking requests, reviews and messages.

***Level 1 Data Flow Diagram***

The system decomposes into six top-level processes, each matching one of the [[AD-04 Input Process Output Charts|AD-04 IPO charts]]. To keep the diagram readable, the seven physical tables from the [[AD-05 Entity Relationship Diagrams|ERD]] are grouped into five logical data stores.

``` mermaid
--- 
title: YourCatsAndDogs Level 1 Data Flow Diagram
config:
  flowchart:
    useMaxWidth: true
--- 
flowchart TD
    PO[Pet Owner]
    PS[Pet Sitter]

    P1((1<br/>Authenticate User))
    P2((2<br/>Manage Pets & Care))
    P3((3<br/>Manage Bookings))
    P4((4<br/>Search))
    P5((5<br/>Manage Reviews))
    P6((6<br/>Manage Messages))

    D1[(D1 Users)]
    D2[(D2 Pets & Care Types)]
    D3[(D3 Bookings & Requests)]
    D4[(D4 Reviews)]
    D5[(D5 Messages)]

    PO -->|credentials| P1
    PS -->|credentials| P1
    P1 -->|session or error| PO
    P1 -->|session or error| PS
    P1 -->|new user record| D1
    D1 -->|stored credentials| P1

    PO -->|pet & care details| P2
    P2 -->|listing confirmation| PO
    P2 -->|pet & care records| D2
    D2 -->|pet & care details| P2

    PO -->|booking window, confirm sitter| P3
    PS -->|booking application| P3
    P3 -->|applicants, confirmation| PO
    P3 -->|application status| PS
    P3 -->|booking & request records| D3
    D3 -->|booking & request details| P3
    D2 -->|pet ownership| P3

    PO -->|sitter search| P4
    PS -->|pet search| P4
    P4 -->|sitter results| PO
    P4 -->|pet results| PS
    D1 -->|user profiles| P4
    D2 -->|pet listings| P4
    D3 -->|open bookings| P4
    D4 -->|review scores| P4

    PO -->|review| P5
    PS -->|review| P5
    P5 -->|confirmation| PO
    P5 -->|confirmation| PS
    P5 -->|review record| D4
    D3 -->|booking details| P5

    PO -->|message| P6
    PS -->|message| P6
    P6 -->|message| PO
    P6 -->|message| PS
    P6 -->|message record| D5
    D5 -->|thread history| P6
```

The processes are:
1. **Authenticate User** — registers new accounts and validates login credentials against `D1 Users`.
2. **Manage Pets & Care** — lets a pet owner list a pet and describe its care needs, stored in `D2 Pets & Care Types`.
3. **Manage Bookings** — the core booking lifecycle: an owner opens a booking window, a sitter applies, and the owner confirms one applicant, all against `D3 Bookings & Requests` (and reading pet ownership from `D2`).
4. **Search** — lets an owner search for sitters and a sitter search for pets needing care, reading across `D1`, `D2`, `D3` and `D4`.
5. **Manage Reviews** — lets either party rate and comment on the other after a confirmed booking, stored in `D4 Reviews`.
6. **Manage Messages** — lets an owner and sitter exchange messages, stored in `D5 Messages`.
