
**Date:** 29 Oct 2025  
**Project:** Student Portal Revamp  
**Module:** Flask-based login system with PostgreSQL backend

**What I did:**
- Refactored `/login` route to use parameterized SQL queries via SQLAlchemy to prevent SQL injection.
- Replaced plaintext password comparison with `werkzeug.security.check_password_hash`.
- Added Flask-WTF form validation for login inputs (email format, password length).
- Created a reusable `User` model with `get_by_email()` and `verify_password()` methods.

**Why I did it:**
- Security audit flagged direct SQL string interpolation in login logic.
- Plaintext password comparison was a major vulnerability.
- Form validation improves UX and prevents malformed requests from hitting the DB.

**Challenges:**
- SQLAlchemy’s session handling was tricky — had to wrap queries in `try/except` to catch `NoResultFound`.
- Flask-WTF clashed with existing HTML templates; needed to refactor form rendering logic.
- Forgot to commit the migration after adding `last_login` column — caused silent failures on staging.

**Next steps:**
- Add `last_login` timestamp update on successful login.
- Write integration tests for login flow using Flask’s test client.
- Review other routes for unsafe SQL patterns.

**Reflection:** 
This was a satisfying cleanup. The login flow is now secure and modular. Learned a lot about SQLAlchemy’s ORM quirks and Flask-WTF’s rendering pipeline. Also reminded myself: always run `flask db migrate && flask db upgrade` before pushing to staging!
