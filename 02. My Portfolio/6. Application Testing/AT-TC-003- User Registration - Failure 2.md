
**Test Case ID:** TC-003

**Description:** Verify that the user cannot use existing email to create the new account

**Preconditions:**
- The Register page is available
- user app-user exists in the database
- user with email a@bc.com already exists in the database

**Steps:**
1. Navigate to http://127.0.0.1:8000
2. Select "Register" in the menu
3. Enter the inputs in the Register form
4. Click "Register"
 
**Test Data:** 
- username: app-user
- email: 123@ok.com
- password: TstUsrP@ss

**Expected Result:** 
- User is unable to register a new account.
- Error message indicates user app-user already registered.