**Reviewer Name:** Emil
**Date:** 26 Nov 2025
**Module/Feature:** Transaction Manager – Add Transaction Function

**Code Summary:**  
This function records a new transaction, validates input, and stores it in the SQL database.

**Strengths:**

- Clear variable naming (`amount`, `category`, `transaction_id`) improves readability.
- Input validation prevents empty fields and incorrect data types.
- Passwords and user IDs are handled securely with parameterised queries.

**Issues Found:**

- Error handling is minimal; exceptions are caught but not logged. Tracked as GitHub Issue #1.
- No unit tests are linked to this function, reducing confidence in reliability.
- Code duplication exists in validation logic across multiple functions. Tracked as GitHub Issue #2.

**Recommendations:**

- Implement structured error logging to assist debugging.
- Add unit tests for boundary cases (e.g., zero amount, invalid category).
- Refactor validation into a reusable helper function.

**Overall Rating:** 
Excellent – strong design, minor refinements needed for robustness.
