# Britve DB Automation

**Microsoft SQL Server Management for DB Owner**

This permission dir provides Bash scripts to manage MS SQL identities, specifically for adding and removing a user with set permissions on the MS SQL Server.

**Overview**

This script automates the process of creating a new SQL Server login and database user based on an email address. It generates a random password for the new user, assigns them full administrative privileges in the specified database, and outputs the connection string for the new user.

**Prerequisites**

sqlcmd tool installed. Refer to this link for more details.
openssl installed for password generation.
Environment variables MYSQL_HOST, MYSQL_URL, MYSQL_USER, SECRET must be set in the profile via the Britive UI. Britive rEsource management configuration must include these variables to successfully run this routine.
MYSQL_HOST: The name of the SQL Server.
MYSQL_URL:Connection string of the SQL Server.
MYSQL_USER: The administrator username with sufficient privileges to create logins and users.
SECRET: The password for the administrator.
Script Functionality

**Checkout Script checkout_script.sh**

Password Generation: The script includes a function generate_password to create a random 12-character password.
User Creation: The script:
Extracts the prefix from the provided email to use as the new SQL Server login and user.
Generates and displays a random password for the new user.
Executes SQL commands to create the login in the master database.
Creates the corresponding user in the specified target database with full admin privileges (db_owner).
Connection String: The script outputs the connection string for the newly created user, which can be used to connect to the SQL Server.

**Checkin Script checkin_script.sh**

User Identification: The script extracts the prefix from the provided email to determine the username to be deleted.
Session Termination:
Queries active sessions for the specified user.
Iterates through each session ID and terminates it using the KILL command to ensure no active connections remain.
User Deletion:
Executes SQL commands to drop the user from the specified database if it exists.
Drops the associated login from the master database.

**Notes**
The generated password and connection string will be displayed in the Britive checkout output.

