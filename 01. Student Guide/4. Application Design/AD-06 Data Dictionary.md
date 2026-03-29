In this section, include:
- A Data Dictionary to describe all the entity attributes (excluding primary and foreign keys) shown on the design of the database schema.

### Example<hr>

Data Dictionary for attributes of entities in the database schema.

***User***

| Attribute    | Data Type | Bytes | Description                                                             | Example             |
| ------------ | --------- | ----- | ----------------------------------------------------------------------- | ------------------- |
| name         | String    | 256   | A free text name (actual name, initials, user selected username, etc.). | johnd, John Doe     |
| email        | String    | 64    | A valid email address.                                                  | john@abc.com        |
| pwd_hash     | String    | 128   | bycript hash of a password                                              | 5d41402abc4b2a76... |
| member since | Timestamp | 8     | The date and time when the user created their account.                  | 03/10/2025 16:38.42 |

***Transaction***

| Attribute | Data Type | Bytes | Description                                                                              | Exaemple   |
| --------- | --------- | ----- | ---------------------------------------------------------------------------------------- | ---------- |
| amount    | Float     | 4     | Monetary amount. Negative values indicate outflow and positive indicate inflow of funds. | $56.25     |
| date      | Date      | 4     | The date of the transaction.                                                             | 12/03/2025 |
| note      | String    | 256   | Free text to describe the transaction.                                                   | New sheos. |


