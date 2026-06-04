==***IN PROGRESS/DRAFT**==

Data dictionary that corresponds to the BreakingBad's Entity Relationship Diagram is shown below.

***User***

| Attribute       | Data Type | Bytes | Description                               | Example              |
| --------------- | --------- | ----- | ----------------------------------------- | -------------------- |
| username        | String    | 256   | Unique user name provided at registration | johnd, John Doe      |
| email           | String    | 64    | A valid and unique email address          | user@address.com     |
| password_hash   | String    | 128   | bcript hash of a password                 | 5d41402abc4b2a761223 |
| password_salt   | String    | 128   | bcript salt of a password                 | 243262243132242e786c |
| default_profile | TEXT      | 64    | type of profile                           | pet_owner/pet_sitter |
