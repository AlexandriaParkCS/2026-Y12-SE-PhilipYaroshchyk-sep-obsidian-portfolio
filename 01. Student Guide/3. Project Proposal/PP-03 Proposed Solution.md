This section describes:
- the software product and how it will solve the problem.
- the software product features, including functional, performance, security etc.
- the user experiences with the software product.
- the 3rd-party software and hardware technologies that will be used.

Ideally, you would link the proposed solution to the Product Statement and Product Features in the Project Vision: 
- [[01. Student Guide/2. Project Vision/PV-03 Product Statement]]
- [[01. Student Guide/2. Project Vision/PV-06 Product Features]]

### Example<hr>

BudgetWise will be a Python-Flask-based Progressive Web Application (PWA) that allows users to:
- Register and log in securely
- Record income and expenses
- Categorise transactions (e.g., food, transport, savings)
- Set and monitor savings goals
- View summaries and trends via charts

***Key Features***
The key features of BudgetWise are:
- Functional:
	- User authentication, financial dashboard, financial transactions, goal tracking, category filtering.
- Performance
	- Fast load times, responsive user interface, offline access via service workers.
- Security
	- Password hashing, input validation, session management, protection against SQL injection.
- Privacy
	- Compliance with the Australian Privacy Act 1988.

***User Experience***
The interface will be clean and intuitive, designed with mobile-first principles. Users will be able to access the application from any device, with offline functionality enabled through PWA caching. Visual feedback (e.g., charts, progress bars) will support financial awareness and motivation.

***Technologies***
BudgetWise will be based on the following 3rd-part technologies:
- Backend: Python, Flask
- Frontend: HTML5, CSS3, Bootstrap, JavaScript
- Database: SQLite
- Authentication: Flask-Login
- Offline support: Service Workers, Web App Manifest

