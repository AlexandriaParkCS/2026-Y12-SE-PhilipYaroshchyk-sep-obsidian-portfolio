***New User Sign Up Experience

Users can access application's main page only. New users are required to sign up by providing their name, email, and password. User name and email must be unique - this ensures easy user identification within the app. Password is masked to prioritise the security.

![[registration.drawio.png]]

Upon successful registration, user is redirected to login page - they now need to login to the application to access its features.

Application displays an error message when the user attempts to use the user name or email that has already been registered in the app. User can proceed with registering their account using another username/email.

![[registration-error.drawio.png]]


***Existing User Login Experience***

Registered users can access the app by entering their username and password. Upon successful verification, the user is logged into the app and navigated to their user profile page.

![[login.drawio 2.png]]

Application displays an error message when the user attempts to login using invalid credentials.

![[login-error.drawio.png]]


***User Profile***

User is able to update their profile by providing their postcode, modify their email address and adding a brief "about section"

![[update-profile.drawio.png]]

***Adding pets***

If user has pets the would like to register with the app, they can do so by adding a pet on their home profile page. They must provide name, species, breed and pet's year of birth. 

![[add-pet.drawio.png]]Once added, user profile shows user's pets on their profile page

***Pet details**

User can navigate to each of their pet details by clicking details button against the pet they would like to access.

![[navigate-to-pet-details.drawio.png]]Pet details page contains information about the pet as well as an option to add types of care that the pet might require, for example walking, feeding, playing with, etc. Also, user can request a booking in the same location.

User can add pet care type entries by filling in the care type form.

![[add-pet-care-type.drawio.png]]App supports multiple care types for each pet to provide more flexibility.

Finally, the pet owner can request a booking for their pet by providing the start date, end date and their desired daily price. Once form is submitted, pet details page shows request as pending (awaiting sitter)

![[request-booking.drawio.png]]

***Search pets to sit***

Pet sitters can search for booking request by providing pet's name, species or breed. They can also optionally provide min and max daily charge.
![[find-pets-to-sit.drawio.png]]
Application returns all pets that have booking requests. Details include pet name and year of birth, owner name and postcode, as well as booking dates and the daily rate. 

Sitter can apply for booking if details match their preferences.

***Confirm pet sitter's request***

Multiple pet sitters can apply for the same booking request while booking is not finalised. Booking is only finalised when the pet owner confirms it upon reviewing pet sitter requests on their pet's page:

![[confirm-booking.drawio.png]]

Once the booking is confirmed, details are shown on pet's page. Alternatively, user can choose to message the pet sitter to find out some details first.

***Access booked sittings***
Pet sitters can navigate their confirmed bookings via clicking "My sittings" in the application menu. Bookings include past and present entries.

![[my-sittings.drawio.png]]
Sitter can leave a review of the pet owner here as well. It is important that both pet owners and pet sitters can rate each other.

***Messaging***

Users can navigate to their message history by clicking "Messages in the " application menu. User can navigate to any of existing conversations by clicking on the link. Once navigated, users see the message history and they can also enter new messages.

![[messaging.drawio.png]]