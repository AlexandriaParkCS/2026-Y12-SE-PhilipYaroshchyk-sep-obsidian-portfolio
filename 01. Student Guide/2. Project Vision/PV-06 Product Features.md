List and briefly describe the product features. Features are the high-level capabilities of the system that are necessary to deliver benefits to the users. Each feature is an externally desired service that typically requires a series of inputs to achieve the desired result. For example, a feature of a problem tracking system might be the ability to provide trending reports.

Because the Vision is reviewed by a wide variety of involved personnel, the level of detail needs to be general enough for everyone to understand.

### Example <hr>

## Core Features

- **User Authentication:** Secure login and registration using hashed passwords.
- **Transaction Recording:** Add, edit, and delete income and expense entries.
- **Categorisation:** Assign transactions to categories such as Food, Transport, or Savings.
- **Dashboard Visualisation:** Real‑time summaries including income, expenses, balance, and category breakdowns.
- **Savings Goals:** Create and track progress toward financial goals.
- **Recent Activity Feed:** Display latest transactions for quick review.

## Supporting Features

- **Responsive Interface:** Works across desktop and mobile devices.
- **Data Validation:** Ensures accuracy and prevents invalid entries.
- **Secure Storage:** All user data stored in a protected SQL database.
- **Error Messaging:** Clear feedback for invalid inputs or failed actions.

## Constraints

- The system must use secure password hashing (e.g., bcrypt).
- The database must support relational integrity between users, transactions, and goals.
- The interface must remain simple and accessible for young users.
- The application must operate within the capabilities of standard web browsers.

## Assumptions

- Users have basic digital literacy and access to an internet‑enabled device.
- Users will enter financial data honestly and consistently.
- The system will be deployed in an educational or personal‑use context, not for enterprise‑level accounting.
- Future enhancements (e.g., recurring transactions, notifications) may be added without major architectural changes.
