==***IN PROGRESS/DRAFT**==

``` mermaid
--- 
title: YourCatsAndDogs Entity Relationship Diagram (DRAFT ONLY)
--- 
erDiagram
    users one -- many pet_sitter_info : has
    users {
        INTEGER id PK
        TEXT username
        TEXT email
        TEXT password_hash
        TEXT password_salt
        TEXT default_profile
    }
    pet_sitter_info {
        INTEGER id PK
        INTEGER user_id FK
        TEXT tba 
    }
    users one -- many pet_owner_info : has
    pet_owner_info {
	    INTEGER id PK
	    INTEGER user_id FK
	    TEXT tba
    }
```