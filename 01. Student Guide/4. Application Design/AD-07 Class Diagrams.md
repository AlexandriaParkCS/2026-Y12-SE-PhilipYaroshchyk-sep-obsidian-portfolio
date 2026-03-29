In this section, include:
- At least one UML style class diagram to show aspects of the  internal structure of the application. This is the only UML (industry standard) diagram that you will create. Note that, in this case, the Class Diagrams must be consistent with the DFDs and Structure Charts (after all, they are all describing the same application).

### Example<hr>

***Transaction Management***
The following class diagram for the Transaction Management process models the key objects and their relationships that support secure, user-specific financial tracking.


![[Transaction Management UML Class Diagram.png]]


The User class represents individuals who register and interact with the application. Each user can track multiple Transactions, each in a different user defined Category. Goals enable users to set savings targets and monitor their progress toward the targets.

The relationships between the entities ensure data integrity and enable efficient querying of user-specific financial data. For example, the system can retrieve all transactions and goals associated with a particular user to generate personalised dashboards and progress summaries.
