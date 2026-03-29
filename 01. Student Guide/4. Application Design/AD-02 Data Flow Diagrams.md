In this section, include:
- A Context Diagram (Level 0 DFD) to identify the external entities (users or otherwise) that will interact with the application and the interfaces that each will use.
- A top level data flow diagram (Level 1 DFD) to show the flow of data and its processing through the application.
- You may create a second level data flow for the processes shown on the top level (Level 1) if you wish to further define the process.

Each diagram should be accompanied with a description.

### Example<hr>

***Context Diagram***
The application interacts with a number of external entities (actors) as shown on the following Context Diagram.

![[BudgetWise DFD Level 0.png]]

The actors include:
- Student: a person who registers, logs in, and interacts with the application to manage their budget. They input income/expense data and receive feedback via dashboards.
- Authentication Provider: a 3rd-party authentication and authorisation provider such as Google. 
- Database: the application uses an SQL database such as SQLite to store financial information for each user.

***Level 1 Data Flow Diagram***
The following diagram shows the top level structure of the application.


![[BudgetWise DFD Level 1.png]]

Users must register and subsequently login with the applicating in order to manage budgets. To register and login, users must provide valid 3rd-part credentials, such as a Google credentials. 

The user are  presented with a dashboard if authorised to manage budgets. The information shown on the dashboard reflects the expenses and income balances previously entered by the user. Active dashboards are cached to optimise performance.

Users can manage budgets and associated income and expenses via the dashboard. The application use ACID transactions to update budget balances both in the database and the dashboard cache.

