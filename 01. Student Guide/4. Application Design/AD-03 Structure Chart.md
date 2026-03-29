In this section, include:
- Structure Charts for at least one of the processes shown on the top level data flow diagram (Level 1 DFD).
- Pseudocode showing the operation of the main process and at least one of the subprocesses.
- Flowchart showing the operation of at least one subprocess that is not covered by pseudocode.

Each diagram should be accompanied with a description.

### Example<hr>

***Dashboard Generation***
The Dashboard Generation process is responsible for producing personalised financial summaries in the application. This process is initiated when a user requests to view their dashboard, typically after logging in.


![[Generate Dashboard Structure Chart.png]]


At the top of the hierarchy is the Generate Dashboard module, which coordinates all submodules to retrieve, process, and present relevant financial data. It delegates tasks to three key data retrieval modules: Get User Data, Get Transactions, and Get Goals. These modules access the SQL database to collect the user’s profile, financial records, and savings goals, respectively.

Once data is retrieved, it is passed to processing modules. Categorise Transactions organises financial entries into meaningful groups (e.g., Food, Transport, Savings), while Calculate Goal Progress compares current savings against user-defined targets.

The data summaries are then used to create tables and charts which visualise spending patterns and goal progress.

Algorithms:

`BEGIN GenerateDashboard`
	`UserSummary = GetUserData(UserID)`
	`TransactionSummary = GetTransactions(UserID)`
	`GoalSummary = GetGoals(UserID)`
	``
	`DISPLAY UserSummary`
	`IF TransactionSummary is empty`
		`DISPLAY Let's start budgeting!`
	`ELSE`
		`DISPLAY TransactionSummary`
	`ENDIF`
	`IF GoalSummary is empty`
		`DISPLAY Let's set some savings goals!`
	`ELSE`
		`DISPLAY GoalSummary`
	`ENDIF`
`END`

`BEGIN GetTransactions`
	`TransactionQuery = SELECT Transactions for UserID`
	`Transactions = RetrieveTransactions(TransactionQuery)`
	``
	`CategorisedTransactions = CategoriseTransactions(Transactions)`
	``
	`SummaryRow = 0`
	`FOR Category in CategorisedTransactions`
		`TRansactionSummary[SummaryRow] = Category`
		`NEXT CategoryRow`
			`FOR Transaction in Category`
				`TransactionSummary[SummaryRow] = Transaction`
				`NEXT CategoryRow`
			`ENDFOR`
	`ENDFOR`
	``
	`RETURN TransactionSummary`
`END`



![[Categorise Transactions Flow Chart.png]]

