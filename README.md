# **CivicPulse - Citizen Engagement Portal**

## **_Overview_**

CivicPulse is a Java-based application designed to enhance citizen engagement with government authorities through a participatory platform. It enables citizens to report issues, submit proposals, vote, comment, and file grievances, while allowing authorities to manage submissions and vendors to handle assigned tasks. The application features a Swing-based graphical user interface (GUI) and integrates with a MySQL database for data persistence.

### **_Key Components_**
- **Backend**: `CivicPulse.java` manages database interactions, business logic, and user management.
- **Frontend**: `CivicPulseGUI.java` provides a user-friendly Swing GUI for system interaction.

### **_User Roles_**
- **Citizen**: Can report issues, submit proposals, vote, comment, file grievances, and view their dashboard.
- **Authority**: Can review issues, assign vendors, select quotations, review work completion, resolve grievances, view dashboards, and generate reports.
- **Vendor**: Can submit quotations, update work progress, mark tasks as completed, and view their dashboard.

---

## **_Prerequisites_**

Before setting up and running CivicPulse, ensure the following requirements are met.

### **_Software Requirements_**
- **Java Development Kit (JDK)**: Version 8 or higher (JDK 17 recommended). Download from [Oracle](https://www.oracle.com/java/) or [OpenJDK](https://openjdk.java.net/).
- **MySQL Server**: Version 5.7 or higher. Download from [MySQL](https://dev.mysql.com/downloads/mysql/).
- **MySQL JDBC Driver**: `mysql-connector-java` (version 8.0.33 recommended). Download from [MySQL Connector/J](https://dev.mysql.com/downloads/connector/j/) or use a dependency manager like Maven.
- **Operating System**: Windows, macOS, or Linux.
- **Command-Line Interface (CLI)**: For compiling and running the application (e.g., Command Prompt on Windows, Terminal on macOS/Linux).

### **_Hardware Requirements_**
- **RAM**: Minimum 4GB (8GB recommended).
- **Storage**: At least 500MB of free disk space for the application, database, and dependencies.

### **_Dependencies_**
- **MySQL JDBC Driver**: Ensure `mysql-connector-java.jar` is included in your classpath.
- If using Maven, add the following to your `pom.xml`:
  ```xml
  <dependency>
      <groupId>mysql</groupId>
      <artifactId>mysql-connector-java</artifactId>
      <version>8.0.33</version>
  </dependency>


Setup Instructions
Follow these steps to set up and run the CivicPulse application.
Step 1: Clone or Download the Project

Clone the project from a version control system (e.g., GitHub):git clone <repository-url>
cd CivicPulseApp


Alternatively, download the project as a ZIP file and extract it to C:\Intel\CivicPulseApp.

Step 2: Set Up the MySQL Database

Install MySQL Server:

Follow the installation instructions for your operating system.
Ensure MySQL Server is running:mysql -u root -p

Enter your root password (default may be empty for local installations).


Create the Database:

Log in to MySQL:mysql -u root -p


Create the civic_pulse database:CREATE DATABASE civic_pulse;
USE civic_pulse;




Create the Database Schema:

Run the provided civic_pulse_schema.sql script:mysql -u root -p civic_pulse < civic_pulse_schema.sql


The schema includes tables: citizens, vendors, authorities, issues, proposals, comments, grievances, quotations, and assignments.


Verify the Database Setup:

Check the tables:USE civic_pulse;
SHOW TABLES;




Update Database Credentials:

Open src/com/civicpulse/system/CivicPulse.java.
Update the database connection details:String url = "jdbc:mysql://localhost:3306/civic_pulse";
String user = "root";
String password = "your_password";

Replace your_password with your MySQL root password. Adjust the url if needed.



Step 3: Add the MySQL JDBC Driver

Download the Driver:

Download mysql-connector-java-8.0.33.jar from MySQL Connector/J.
Place it in the lib directory (e.g., C:\Intel\CivicPulseApp\lib).


Update the Classpath:

Include the JAR file in the classpath when compiling and running (see below).



Step 4: Compile and Run the Application

Navigate to the Project Directory:
cd C:\Intel\CivicPulseApp


Compile the Application:

Create the bin directory for compiled classes:mkdir bin


Compile all Java files:javac -d bin -sourcepath src -cp lib\mysql-connector-java-8.0.33.jar src\com\civicpulse\gui\CivicPulseGUI.java src\com\civicpulse\system\CivicPulse.java




Run the Application:

Run the application:java -cp bin;lib\mysql-connector-java-8.0.33.jar com.civicpulse.gui.CivicPulseGUI

On macOS/Linux, use:java -cp bin:lib/mysql-connector-java-8.0.33.jar com.civicpulse.gui.CivicPulseGUI


The GUI window titled "Civic Pulse - Citizen Engagement Portal" should appear.




Project Structure
CivicPulseApp/
├── src/
│   ├── com/
│   │   ├── civicpulse/
│   │   │   ├── core/
│   │   │   │   └── Category.java        # Enum for issue categories
│   │   │   ├── gui/
│   │   │   │   └── CivicPulseGUI.java   # Swing-based GUI
│   │   │   ├── system/
│   │   │   │   └── CivicPulse.java      # Backend logic
│   │   │   ├── user/
│   │   │   │   ├── model/
│   │   │   │   │   ├── User.java        # Base user class
│   │   │   │   │   ├── Citizen.java     # Citizen user model
│   │   │   │   │   ├── Authority.java   # Authority user model
│   │   │   │   │   ├── VendorUser.java  # Vendor user model
│   │   │   │   │   └── Role.java       # Enum for user roles
│   │   │   │   └── profile/
│   │   │   │       └── Vendor.java      # Vendor profile class
├── lib/
│   └── mysql-connector-java-8.0.33.jar  # MySQL JDBC driver
├── bin/
│   └── (compiled .class files)
├── civic_pulse_schema.sql               # Database schema script
└── README.md                            # This file

Key Files

CivicPulseGUI.java: Swing-based GUI with forms for registration, login, and dashboards.
CivicPulse.java: Handles database connections, authentication, and core functionalities.
civic_pulse_schema.sql: SQL script to create the database schema.


Usage Guide
Launching the Application

Run the application to display the main window.
Select a user type ("1. Citizen", "2. Authority", or "3. Vendor") and click "Proceed".

Citizen Workflow

Select "1. Citizen" and click "Proceed".
Register or Login:
Register with details (e.g., username: bob, password: bob123).
Login with credentials.


Citizen Dashboard:
Report Issue: Submit an issue (e.g., issueId: 1, description: "Pothole").
Submit Proposal: Create a proposal.
Vote/Comment/File Grievance: Interact via console.
View Dashboard: Review your submissions.
Logout: Return to the main menu.



Authority Workflow

Select "2. Authority" and click "Proceed".
Login: Use credentials (e.g., admin/admin123).
Authority Dashboard:
Review Issues/Assign Vendor/Select Quotation/Resolve Grievance: Manage via console.
View Dashboard/Generate Report: Review data.
Logout: Return to the main menu.



Vendor Workflow

Select "3. Vendor" and click "Proceed".
Register or Login:
Register (e.g., username: vendora, expertise: SANITATION).
Login with credentials.


Vendor Dashboard:
Submit Quotation/Update Progress/Mark Completed: Manage via console.
View Dashboard: Review assignments.
Logout: Return to the main menu.




Testing Instructions
Test Case 1: Citizen Registration and Issue Reporting

Launch the application, select "1. Citizen", and register (e.g., username: alice, password: alice123).
Login and report an issue (e.g., issueId: 1, description: "Pothole").
Verify the issue in the dashboard.

Test Case 2: Vendor Registration and Quotation Submission

Select "3. Vendor", register (e.g., username: vendorb, expertise: INFRASTRUCTURE).
Login and submit a quotation for issueId 1.
Verify the submission.

Test Case 3: Authority Login and Issue Assignment

Select "2. Authority", login (e.g., admin/admin123).
Review and assign issueId 1 to a vendor.
Verify the assignment.


Troubleshooting
Common Issues

ClassNotFoundException: com.mysql.cj.jdbc.Driver:
Ensure mysql-connector-java-8.0.33.jar is in the classpath.


SQLException: Access denied:
Verify credentials in CivicPulse.java.


SQLException: Table doesn't exist:
Run civic_pulse_schema.sql.


Duplicate entry for key 'PRIMARY':
Use unique IDs for issues/proposals.




Contribution Guidelines

Fork and Clone:git clone <your-fork-url>
cd CivicPulseApp


Create a Branch:git checkout -b feature/your-feature-name


Make and Test Changes:
Follow existing code style.
Test thoroughly.


Commit and Push:git add .
git commit -m "Add feature: description"
git push origin feature/your-feature-name


Create a Pull Request:
Submit a pull request with a clear description.



Code Style

Use 4-space indentation.
Follow Java naming conventions.
Comment complex logic.
Handle exceptions with user-friendly messages.


Future Improvements

Enhanced GUI: Replace console interactions with GUI forms.
Input Validation: Add robust form validation.
Logging: Implement event and error logging.
Testing: Add JUnit tests.
Security: Hash passwords.
Scalability: Optimize queries and add indexing.


License
This project is licensed under the MIT License. See the LICENSE file for details.

Contact
For questions or support, contact the maintainers at:

2023ayush.kumar@vidyashilp.edu.in
2023pruthvi.raj@vidyashilp.edu.in



