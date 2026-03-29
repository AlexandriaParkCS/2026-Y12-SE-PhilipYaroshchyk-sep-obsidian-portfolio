In this section, include:
- At least one Entity Relationship Diagram (ERD) that captures part of the (relational) database schema of the database that will be used by the application.

The ERDs must show your skills to document one-to-one and one-to-many relationships between at least three entities. It is recommended to show the complete design of the application's database schema as this will simplify the implementation of the schema.

There are several notation systems for ERDs. They are similar but very in few specifics. Use the Crow's Foot (a.k.a. Martin or Information Engineering) notation. Alternatively, you may take a contemporary approach and use the UML notation to create a model of the entities and their relationships.

### Example<hr>

The application will store its data in an SQL database with the following structure:


![[BudgetWise ERD.png]]

The model supports secure user accounts, financial tracking, and goal-setting functionality. 

The User entity represents individuals who register and interact with the application. Each user can track multiple Transactions, each in a different user defined Category. Goals enable users to set savings targets and monitor their progress toward the targets.

The relationships between the entities ensure data integrity and enable efficient querying of user-specific financial data. For example, the system can retrieve all transactions and goals associated with a particular user to generate personalised dashboards and progress summaries.
