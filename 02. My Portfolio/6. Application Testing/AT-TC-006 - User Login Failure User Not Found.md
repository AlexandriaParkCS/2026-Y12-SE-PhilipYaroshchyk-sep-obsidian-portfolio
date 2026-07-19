
**Test Case ID:** TC-006

**Description:** Verify that the user cannot login to their when providing incorrect password

**Preconditions:**
- The Login page is available
- User test1000 does not exist in the database

**Steps:**
1. Navigate to http://127.0.0.1:8000
2. Select "Login" in the menu
3. Enter the inputs in the Login form
4. Click "Login"
 
**Test Data:** 
- username: test1000
- password: anyPass

**Expected Result:** 
- User remains on the login page
- Error message is displayed showing "incorrect credentials"