In this section, include:
- An Input Output Process (IPO) chart for at least one of the of the processes shown on the top level data flow diagram (Level 1 DFD).

If your structure charts are covering only some of the processes on the Level 1 DFD, then select a process which is not covered by a structure chart and create an IPO chart for it.

### Example<hr>

***Login/Register***
The Login/Register process is a critical component of the application, enabling secure access and personalised user experiences. This process allows new users to create accounts and existing users to authenticate their credentials to access their budgeting data.

Summary of a user login:

*Input*
	- Full Name
	- Email address
	- Password (plain text)

*Process*
	- Sanitise and validate the full name, email address and password
	- Calculate a password hash
	- Check for an existing user using the email address
	- If it exists, retrieve the stored password hash, otherwise reject the login 
	- Compare the stored and calculated password hashes
	- If the the password hashes match, initialise a user session
	- Otherwise, allow entry of another password (up to 3 attempts), or prevent login attempts for 5 minutes (after 3 attempts)
*Output*
	- Success message
	- Error message, if required
	- Authentication session token

Summary of user registration:
...

