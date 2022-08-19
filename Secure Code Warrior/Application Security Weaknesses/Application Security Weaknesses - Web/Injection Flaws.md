---
tags: [data_handling]
---
# Injection Flaws
## Code Injection
### Context
Application uses a programming language and displays a form of user input. Attackers could potentially abuse the system that trusts the input and inject a piece of code into the system and tamper with the initial logic 
### Danger
Danger usually is high when attackers can inject code. Basically, the whole [[Business Logic]] could be rewritten or bypassed. Sensitive data could also be retrieved, or user rights could be elevated
### Example
A calculator application displays a text prompt where users are expected to enter integers. If the user enters code instead, the code might be executed on server-side, leading to file retrieval
### Counter Measures
- Never [[Trust no Input|trust input]]
- Use parameterised queries
- Apply [[Least privilege]], such as read-only server and client
- Use application-wide filters and sanitisation on all user-provided input, using filtering, encoding, allow-list validation
- Do not let functions interpret or execute user input directly
## HTTP Injection (CRLF Injection)
### Context
Carriage Return and Line Feed (CRLF), which are used for line termination, can be exploited.
When an user input allows CRLF injection, 
### Danger
Attackers could exploit the vulnerability in various ways, but the most important one is enabling [[Phishing]] attacks 
### Example
Note: In a HTML encoding, `%0d` is the character carriage return, and `%0a` is the character line feed. Together, they are interpreted as "new line"
#### Logic tampering 
A web application keeps a log of the visited URL with a timestamp and the source IP. The attacker appends a CRLF injection to the URL: after the CRLF, he injects a fake log. The administrator will see a suspicious activity and try to investigate
#### Redirection attack
Attacker can also use a CRLF injection flaw to craft a malicious URL: while the first part of the URL contains the vulnerable domain name, the second part can redirect to a malicious HTML content specified by the attacker
### Counter Measures
- Never [[Trust no Input|trust input]]
- Use application-wide filters and sanitisation on all user-provided input, using filtering, encoding, allow-list validation
- Apply HTML encoding to anything sent back to the browser
## LDAP Injection
### Context
Lightweight Directory Access Protocol (LDAP) is a protocol used to fetch user information such as user rights in a directory system. It usually uses TCP/IP protocol, and became a norm for directory management.
LDAP Injecting is the malicious injection of LDAP statement in a query
### Danger
Risks of access with elevated rights are high, and sensitive data could also be leaked
### Example
#### Bypassing authentification
In an application, in the authentification form, an attacker submits an input including LDAP injection. The input is submitted to the backend, and attacker can gain access rights and access to the targeted account: potentially an administrator 
In LDAP statements, `(&)` is interpreted as `True` statement. Because of this statement, the password condition can be ignored
#### Information disclosure
In a query where the user is retrieving his own information using his id, an attacker replaces the id with a wildcard character (`*`). Data of all users will be retrieved, and cause a major information disclosure
### Counter Measures
- Use application-wide filters and sanitisation on all user-provided input, using filtering, encoding, allow-list validation
- Use framework provided functions when available
- Make use of escaped variables in LDAP queries
- Use LDAP injection resistant framework, automatic LDAP encoding
- Perform validation through an allowlist
- Minimise LDAP binding account privileges: apply [[Least privilege|Least privilege principle]]
## NoSQL Injection
### Context
[[NoSQL|Not only SQL (NoSQL)]] refer to a specific category of DataBase Management Systems (DBMS), which emerged in the late 1960s. [[NoSQL]] systems provide storage and retrieval of data modeled in other means than the tabular relations used by SQL DBMS.
NoSQL injection refer to attacks where malicious code is injected into a NoSQL database.
JSON and JavaScript code usually are the main ways to exploit NoSQL Injection.
### Danger
Attackers could be allowed to access, add, or delete data from the database
### Example
In the normal flow, users submit their authentification information through a POST request. Parameters are appended to a database query string submitted to the database. When the credentials are valid, the appropriate record is returned to the web server and the session cookie is returned to the user, who logs in.
If the attacker uses an interception proxy to change input values that change the logic of the query: a NoSQL comparison operator is passed instead of the normal username and password data. The username and password will be compared to an empty string, always resulting in a `True` condition: this will allow the attacker to log in as the first user of the database (possibly the admin)
### Counter Measures
- Input should be JavaScript escaped or validated before being used to query the database
- Apply allow-list validation on all user input
- Use database ORM instead of raw queries
- Apply [[Least privilege|least privilege principle]] on database users
- Validate input parameters, and [[Trust no Input|do not trust user input]]
- Coerce input to the correct types during validation routines
- Use explicit comparison operators such as `$eq` rather than allowing implicit equality matching: for example, use `{field: { $eq: "research key"}` rather than `{field: "research key"}`
## OS Command Injection
### Context
OS Command injection refer to vulnerability where Operating System (OS) commands are allowed to be executed from the application. This happens when user input are passed to the shell system without validation
### Danger
When attackers gain access to OS commands, the whole application could be compromised: data can be retrieved and leaked, or server could be reset and shut off
### Example
In an application, users can specify a file to delete from their profile. If the attacker appends to this parameter a semi-colon to end the shell command, as well as a second instruction, the second instruction can be interpreted as well by the OS. The second command could, for example, delete the server
### Counter Measures
- Use framework specific API calls instead of OS commands
- Validate all user controlled output against an allow-list before passing it to the shell
- Always apply [[Least privilege|least privilege principle]]
## Path Traversal
### Context
An application is contained in a directory folder. Path Traversal is used to access folders outside the web root folder. Ways to use path traversal include manipulating the relative path using `../` sequences, double URL encoding, or absolute paths.

Other names for Path Traversal attacks include:
- Directory Traversal
- Directory Climbing
- Backtracking
- Dot-dot-slash
### Danger
Sensitive files could be accessed by the attacker
### Example
In an application, users can request a file in the application's web server. Using path traversal, instead of retrieving an expected file, the attacker retrieves confidential information, such as passwords
### Counter Measures
- Test path traversal vulnerabilities
- Work without user input when using file system calls
- Use indexes instead of parts of file names
- Restrict user input on parts of the path that should not be modified or accessed
- Use chrooted jails and code access policies to [[Least privilege|restrict modification]]
- Normalise the input
## Local File Inclusion (LFI)
### Context
Local File Inclusion is a vulnerability allowing local files to be executed by forged requests
### Danger
Sensitive information could be retrieved, or remote shell could be executed
### Example
An application web page uses the `page` parameter to dynamically build the content of the page, and loads a local HTML file stored on the server. An attacker forges an URL using [[Injection Flaws#Path Traversal|path traversal]] to access sensitive files
### Counter Measures
- Never pass user input to `file include` commands
- Use indirect reference map
- Apply allow-list against [[Trust no Input|user input]]
- Pay attention to [[Injection Flaws#Path Traversal|../]] or encoded variants in user input
## Remote File Inclusion
### Context
Remote File Inclusion is a vulnerability allowing files hosted on another server to be included or executed on the application server or web page
### Danger
Sensitive data could be retrieved, or the attacker could [[Denial of Service|DoS]] the service. If the URL is sent to a user, [[Phishing|phishing]] could also be a threat
### Example
An application web page uses the `page` parameter to dynamically build the content of the page. An attacker hosts a malicious shell command, and includes their shell command when loading the application web page. The script is executed on the application server, and sensitive data is retrieved by the attacker
### Counter Measures
- Never pass user input to `file include` commands
- Use indirect reference map
- Apply allow-list against [[Trust no Input|user input]]
## SQL Injection
### Context
SQL Injection is a [[Injection Flaws#Code Injection|code injection subcategory]] where attacker specifically uses SQL code to access the database
### Danger
The SQL interpreter could execute arbitrary code: this includes retrieval of sensitive information and deletion of the database, causing data leakage, risk repudiation or [[Denial of Service|DoS]]
### Example
An application requires user authentification. However, instead of entering a password, the attacker injects an SQL code sequence to bypass the password verification using a statement always evaluated to `True`
### Counter Measures
- Use parameterised queries
- Do not [[Trust no Input|trust user input]] and simply concatenate it
- Use framework tools to build database queries
- Use allow-list on user input
- Apply [[Least privilege|Least Privilege principle]] on all database users
## XML Injection
### Context
XML Injection is a [[Injection Flaws#Code Injection|code injection subcategory]] where attacker specifically uses XML code
### Danger
An attacker could gain elevated rights, or tamper with the database
### Example
An application requires user authentification, and thus has a user registration page. The application web server constructs XML based on the text fields used for login and password, and appends it to a database.

On this page, an attacker creates a new user, but appends XML code to the password. The appended XML code creates another user with elevated rights. When the XML string is added to the database, it results in two accounts being created, including one with administrator rights
### Counter Measures
- [[Trust no Input|Sanitise]] user input using built-in framework functions
- Use [[DTD]] or [[XSchema]] validation
## XPath Injection (XQuery Injection)
### Context
XPath is a querying language bound to XML: it is a statement based language that allows XML query to locate a piece of information based on beacons.
XML Injection is a [[Injection Flaws#Code Injection|code injection subcategory]] where attacker specifically exploits XML code to make queries on fields using XPath
### Danger
An attacker could bypass password check and thus access the application as administrator
### Example
An application requires user authentification, and thus has a user registration page. The application web server constructs XML based on the text fields used for login and password, and appends it to a database.

On this page, an attacker creates a new user, but appends XPath queries to the text fields. The malicious code enables the attacker to bypass password verification, and is able to log in as administrator
### Counter Measures
- Use parameterised XPath interface. Include all user inputs such as GET and POST parameters, cookies, and HTTP headers
- [[Trust no Input|Sanitise]] all user input used in XPath expressions from special characters
- Apply [[Least privilege|Least Privilege principle]]: only use read-only user to perform queries that do not need write permissions
## Email Header Injection
### Context
In application allowing emails to be sent, Email Header Injection is a type of attack where additional mail headers can be added
### Danger
Attackers could reveal a secret address, use a diffusion address to launch a large scale [[Phishing]] attack, or modify fixed values in the email body
### Example
An application allows user to send questions to a secret mailbox.
By adding a new line using `%0A` special character (URL encoding), the attacker can add his own email address as secondary recipient.
### Counter Measures
- [[Trust no Input|Never trust user input]]
- Apply filters on user input
- Apply an allow-list for user input
## Deserialisation of Untrusted Data
### Context
Serialisation is the process of translating data structures or object states into a format that can be easily stored, while deserialisation is the opposite process of taking storable format and reforming complex data structure or object states
### Danger
Arbitrary code could be executed, or [[Denial of Service|DoS]] could be inflicted. Depending on how the serialised object is used, [[Injection Flaws#SQL Injection|SQL injection]], [[Cross Site Scripting|XSS]] or remote code execution could threaten the application 
### Example
An application uses serialisation to store users shopping cart. An attacker changes the serialised shopping cart, hoping the application does not check the new attributes
### Counter Measures
- Sanitise the data of a serialised object just like user input: basically [[Trust no Input|Trust no Serialised object]]
- Implement integrity checks, using digital signatures to prevent tampering
- Isolate and run code that deserialises in a low privilege environment
## Log Forging
### Context
Log files are used to form history of events and transactions in applications, or to help debugging. Log Forging is a type of attack where the attacker adds malicious logs.
Log Forging can corrupt the file format, making it harder to analyse logs, or change the history to cover up another attack
### Danger
Log Forging can delay the administrator's response to another attack. While it has limited impact on itself, it acts as an enabler for other more potent threats
### Example
An application logs failed login attempts, and use a count of failures logs to block successive attempts.
While brute-forcing the password, the attacker injects a fake successful login attempt in the log file at regular intervals, and continues brute-forcing the password
### Counter Measures
- Ensure there is client and server side input validation
## Resource Injection
### Context
Resources injection occurs when attackers are able to control and manipulate resource identifiers
### Danger
Sensitive information could be leaked, or services could be tampered or denied
### Example
An attacker notices ports are displayed whenever an HTTP request is made. The application creates a socket without validation of the originating requestor. The attacker can then connect directly and transmit sensitive information to a third-party server or perform [[Denial of Service|DoS]] attack.
### Counter Measures
- Look out for user input that indicate the content type
- Use a list of acceptable inputs that conform strictly to specifications: for example, only accept a determined list of port numbers
- Applications permitting special characters as input should raise a red flag when used alongside methods interacting with the file system
- Data containing URL or URI should raise a red flag when functions can be used to create remote connections
## CSS Injection
### Context
Cascading Style Sheet (CSS) is used pretty much everywhere to add a styling layer to plain HTML.
CSS Injection occurs when arbitrary CSS code is injected into a trusted website and rendered in the victim's browser
### Danger
CSS Injection enables attackers to [[Phishing|phishing attacks]]
### Example
A social networking website allows users to insert CSS to update the background colour. An attacker injects malicious CSS payload and adds a logger to the website. When a [[CSRF]] token matches a snippet included in the injected CSS payload, the code will set the background image to a malicious URL, and the attacker will retrieve the CSRF token
### Counter Measures
- Use context-dependent sanitisation
- Use allow-listing to prevent loading arbitrary style sheets
- Not allow users to customise the CSS of their personal pages
- Implement a Content Security Policy to restrict where images and stylesheets can be loaded from
- Sanitise HTML tags such as style


### Context
### Danger
### Example
### Counter Measures