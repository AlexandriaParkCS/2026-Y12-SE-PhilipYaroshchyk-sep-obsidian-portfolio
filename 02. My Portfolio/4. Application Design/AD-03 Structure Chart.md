***Manage Bookings***

The Manage Bookings process is responsible for the full lifecycle of a booking: a pet owner creates a sitting request for a pet, pet sitters apply to look after it, and the owner confirms one applicant. 

``` mermaid
--- 
title: Manage Bookings Structure Chart
config:
  flowchart:
    useMaxWidth: true
--- 
flowchart TD
    M0[Manage Bookings]

    M1[Create Booking]
    M2[Apply for Booking]
    M3[Confirm Booking]

    M0 --> M1
    M0 --> M2
    M0 --> M3

    M1a[Validate Pet <br/>Belongs to Owner]
    M1b[Validate Dates <br/>and Price]
    M1c[Insert Booking Record]
    M1 --> M1a
    M1 --> M1b
    M1 --> M1c

    M2a[Validate Sitter <br/>Profile Complete]
    M2b[Validate Booking <br/>is Still Open]
    M2c[Insert Booking <br/>Request Record]
    M2 --> M2a
    M2 --> M2b
    M2 --> M2c

    M3a[Validate Request <br/>Belongs to Owner's Pet]
    M3b[Update Booking <br/>with Confirmed Sitter]
    M3 --> M3a
    M3 --> M3b
```

At the top of the hierarchy is the **Manage Bookings** module, which dispatches to one of three submodules depending on who is acting and at what stage the booking is at. **Create Booking** is called by a pet owner to open a sitting window; it validates the pet belongs to the caller and that the supplied dates and price are sensible before inserting an unconfirmed booking. **Apply for Booking** is called by a sitter; it checks their profile is complete and the booking is still open before recording their interest as a booking request. **Confirm Booking** is called by the pet owner to accept one applicant; it checks the request belongs to one of the owner's own pets before updating the booking with the chosen sitter.

***Pseudocode***

Main process:

	BEGIN ManageBookings
		CASE action OF
			"create":  CreateBooking(petId, startDate, endDate, dailyPrice)
			"apply":   ApplyForBooking(bookingId, sitterId)
			"confirm": ConfirmBooking(requestId, ownerId)
		ENDCASE
	END

Subprocess — Create Booking:

	BEGIN CreateBooking(petId, startDate, endDate, dailyPrice)
		Pet = GetPetByIdAndOwner(petId, CurrentUserId)
		IF Pet is NULL
			DISPLAY "Pet not found or no permission"
			RETURN
		ENDIF
		
		Error = NULL
		IF startDate is empty OR endDate is empty OR dailyPrice is empty
			Error = "Missing required field"
		ELSE IF startDate is not a valid date OR endDate is not a valid date
			Error = "Dates must be valid"
		ELSE IF startDate < Today OR endDate < Today
			Error = "Dates cannot be in the past"
		ELSE IF endDate < startDate
			Error = "End date must be after start date"
		ENDIF
		 
		IF Error is NULL
			dailyPrice = Round(dailyPrice)
			INSERT INTO Bookings (petId, sitterId = NULL, startDate, endDate, dailyPrice)
			DISPLAY "Booking added successfully"
		ELSE
			DISPLAY Error
		ENDIF
	END

***Flowchart — Confirm Booking***

Confirm Booking is not covered by the pseudocode above, so its operation is shown as a flowchart instead. It mirrors `confirm_booking()` in `flaskr/home.py`.

``` mermaid
--- 
title: Confirm Booking Flowchart
config:
  flowchart:
    useMaxWidth: true
--- 
flowchart TD
    Start([Start - Confirm Booking Request]) --> Input[/Receive requestId/]
    Input --> Lookup[Look up booking_request joined <br/>with bookings and pets]
    Lookup --> Check{Request exists and pet <br/>belongs to current user?}
    Check -->|No| ErrorMsg[Flash not found or <br/>no permission error]
    ErrorMsg --> Redirect1[Redirect to Home]
    Check -->|Yes| Update[UPDATE bookings <br/>SET sitter_id]
    Update --> Success[Flash Booking confirmed message]
    Success --> Redirect2[Redirect to Pet Detail Page]
    Redirect1 --> End([End])
    Redirect2 --> End
```
