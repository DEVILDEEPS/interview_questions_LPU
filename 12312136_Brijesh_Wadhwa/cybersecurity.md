Cybersecurity Interview Handbook
Part 1 (Questions 1–25)
Python + Networking + Linux
Python
Q1. What is the difference between a list and a tuple in Python?
Answer

Both store ordered collections of data, but there are key differences.

List	Tuple
Mutable	Immutable
Uses []	Uses ()
Slower	Faster
More memory	Less memory

Example

my_list = [1,2,3]
my_list.append(4)

my_tuple = (1,2,3)
# my_tuple.append(4) ❌

Use a tuple when data should never change, such as an IOC represented as (IP, Timestamp).

Follow-up

Why are tuples faster?

Because Python doesn't need to allocate extra memory for modifications.

Q2. Explain *args and **kwargs.
Answer

*args

Allows multiple positional arguments.

def add(*args):
    return sum(args)

add(2,3,5)

**kwargs

Allows multiple keyword arguments.

def user(**kwargs):
    print(kwargs)

user(name="Brijesh", role="SOC")

Useful in Flask APIs where parameters vary.

Q3. What are decorators?
Answer

Decorators modify the behavior of a function without changing its code.

Example

def logger(func):

    def wrapper():
        print("Started")
        func()
        print("Finished")

    return wrapper


@logger
def hello():
    print("Hello")

Output

Started
Hello
Finished

Security tools often use decorators for authentication or logging.

Q4. Difference between deep copy and shallow copy.
Answer

Shallow copy copies references.

Deep copy copies actual objects.

import copy

a=[[1,2],[3,4]]

b=copy.copy(a)

c=copy.deepcopy(a)

If nested objects change,

copy.copy()

may also change.

Deep copy avoids this.

Q5. What are generators?
Answer

Generators produce values one at a time using yield.

def nums():
    for i in range(5):
        yield i

Advantages

Less memory
Faster for large datasets
Ideal for log processing
Q6. What is the difference between Flask and Streamlit?
Answer

Flask

Backend framework
REST APIs
Routing
Authentication

Streamlit

Data dashboards
Visualization
Rapid prototyping

In your Threat Intelligence Platform

Flask handled APIs.
Streamlit displayed enriched IOC dashboards.
Q7. Explain exception handling.
Answer
try:
    x=10/0

except ZeroDivisionError:
    print("Cannot divide")

finally:
    print("Done")

finally always executes.

Security tools use exception handling when API requests fail.

Q8. Difference between multithreading and multiprocessing.
Answer

Multithreading

Shared memory
Lightweight
Best for I/O

Multiprocessing

Separate memory
CPU intensive

Since Nmap spends most of its time waiting for network responses, multithreading is a suitable choice for scanning many hosts concurrently.

Networking
Q9. Explain the OSI Model.
Answer
Layer	Function
Application	HTTP DNS SMTP
Presentation	Encryption
Session	Session control
Transport	TCP UDP
Network	IP Routing
Data Link	MAC
Physical	Cable

Interviewers usually ask:

"Which layer does HTTPS work on?"

Application layer.

TLS encryption operates between Application and Transport.

Q10. TCP vs UDP.
Answer

TCP

Reliable
Connection-oriented
Ordered delivery

UDP

Fast
No acknowledgements
Connectionless

Examples

TCP

HTTPS
SSH
FTP

UDP

DNS
VoIP
Streaming
Q11. Three-way handshake.
Answer

TCP establishes a connection using:

Client

SYN

Server

SYN ACK

Client

ACK

Connection established.

Q12. What happens when you type google.com?
Answer
Browser checks cache.
DNS lookup resolves the IP address.
TCP three-way handshake.
TLS handshake for HTTPS.
HTTP request sent.
Server responds.
Browser renders the page.

This is a very common interview question.

Q13. What is DNS?
Answer

DNS converts domain names into IP addresses.

Example

google.com

↓

142.x.x.x

Without DNS, users would have to remember IP addresses.

Q14. Explain HTTP methods.
Answer

GET

Retrieve data.

POST

Create data.

PUT

Replace data.

PATCH

Modify data.

DELETE

Delete resource.

Your Flask APIs likely used GET for IOC retrieval and POST for submitting indicators.

Q15. Difference between HTTP and HTTPS.
Answer

HTTP

Port 80
Plaintext
Not encrypted

HTTPS

Port 443
Uses TLS
Secure communication
Q16. What is ARP?
Answer

ARP maps an IP address to a MAC address within a local network.

Example

192.168.1.10

↓

00:1A:2B:3C:4D:5E

Attack

ARP Spoofing

Defense

Dynamic ARP Inspection.

Q17. What is NAT?
Answer

Network Address Translation translates private IP addresses into public IP addresses.

Benefits

Conserves IPv4 addresses
Hides internal devices
Linux
Q18. Difference between grep, awk, and sed.
Answer

grep

Searches text.

grep error logs.txt

awk

Processes columns.

awk '{print $1}'

sed

Edits text.

sed 's/http/https/'
Q19. Explain Linux permissions.
Answer
-rwxr-xr--

Owner

rwx

Group

r-x

Others

r--

Permission values

r=4

w=2

x=1

755 means

Owner

7

Group

5

Others

5
Q20. chmod vs chown.
Answer

chmod

Changes permissions.

chmod 755 file

chown

Changes ownership.

chown user file
Q21. How do you find large files in Linux?
Answer
find / -type f -size +100M

Useful for log analysis and storage management.

Q22. What is a process?
Answer

A process is a running instance of a program.

Useful commands

ps

top

htop

kill
Q23. Difference between soft link and hard link.
Answer

Soft Link

Shortcut
Can cross filesystems
Breaks if original is deleted

Hard Link

Same inode
Cannot cross filesystems
Continues to work if original filename is deleted (as long as another hard link exists)
Q24. What is the purpose of the /etc/passwd file?
Answer

It stores user account information such as username, UID, GID, home directory, and login shell.

Example entry:

brijesh:x:1001:1001:Brijesh:/home/brijesh:/bin/bash

Passwords are not stored here on modern Linux systems; they are stored in /etc/shadow, which has restricted permissions.

Q25. What is SSH and why is it secure?
Answer

SSH (Secure Shell) is a protocol for securely accessing remote systems over an encrypted connection, typically using port 22.

Security features:

Encrypts all communication.
Supports password and public key authentication.
Protects against eavesdropping and many man-in-the-middle attacks when host keys are verified.

Example:

ssh user@192.168.1.10
Follow-up

Why is SSH preferred over Telnet?

Because Telnet transmits data, including passwords, in plaintext, while SSH encrypts the entire session.