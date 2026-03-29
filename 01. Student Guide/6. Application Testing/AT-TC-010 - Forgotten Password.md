
**Test Case ID:** TC-010

**Description:** 
Verify that a user can reset their password using a valid email address.

**Preconditions:**
- A user account with a registered email `user@example.com` exists.
- The "Forgot Password" page is accessible.

**Steps:**
1. Navigate to the login page.
2. Click the "Forgot Password?" link.
3. Enter a registered email address in the field.
4. Click the "Submit" button.
 
**Test Data:** 
- Registered email: `user@example.com`

**Expected Result:** 
A success message is displayed, and an email with a password reset link is sent to the registered email address.