
**Test Case ID:** TC-002

**Description:** Verify that the user cannot use existing user name to create the new account

**Preconditions:**
- The Register page is available
- user non-user does not exist in the database
- user with email 123@ok.com does not exist in the database

**Steps:**
1. Navigate to http://127.0.0.1:8000
2. Select "Register" in the menu
3. Enter the inputs in the Register form
4. Click "Login"
 
**Test Data:** 
- Case 2:
	- username non-user
	- email: a@bc.com
	- password: TstUsrP@ss

**Expected Result:** 
- User is unable to register a new account
- Error message indicates user non-user already registered