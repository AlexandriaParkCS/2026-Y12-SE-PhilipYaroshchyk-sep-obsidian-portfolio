
**Test Case ID:** TC-010

**Description:** Verify that the user can add a new pet care type to their pet

**Preconditions:**
- The user has logged in to the app
- The user has onboarded their pet Tommy into the app - see [AT-TC-008 ](obsidian://open?vault=2026-Y12-SE-PhilipYaroshchyk-sep-obsidian-portfolio&file=02.%20My%20Portfolio%2F6.%20Application%20Testing%2FAT-TC-008%20-%20User%20is%20able%20to%20add%20a%20pet)

**Steps:**
1. After login, navigate to the profile page by clicking "Home" in the menu
2. Scroll down to "You pets section"
3. Click on "Details" against Tommy's entry
4. Fill in the "Add new care type" form
5. Click "Add" to submit the form
 
**Test Data:** 
- type of care: "feeding"
- schedule: "twice daily"
- description: "feeding instructions description"

**Expected Result:** 
- Care type entry is added to Tommy's page 