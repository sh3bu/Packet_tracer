1) Login as a root user. 
2) Create two users yourrollnumberamrita(client) and yourrollnumbercoimbatore(server) 
with passwords. 
3) Login as yourrollnumberamrita. Use ssh to create the private and public ids at the 
location /home/yourrollnumberamrita/.ssh 
4) Then copy the public id file to the 
/home/yourrollnumbercoimbatore/.ssh/authorized_keys 
5) Do the necessary steps if required (editing ssh config files and restarting the service, 
providing permissions for .ssh and .ssh/ authorized_keys etc..) 
6) Check are you able to login without a password from yourrollnumberamrita to 
yourrollnumbercoimbatore using ssh 
7) Then switch user to yourrollnumberamrita. 
8) Write a script remoteshell.sh which will do the following sub-tasks 
a) Printing the name of current login user 
b) This step is done based on your roll number. Run a makefile that prints the 
number is (Prime (odd roll number)/Palindrome (even roll number)) using a 
binary file (Prime/Palindrome). Write C program according to your roll number 
and include the linking steps in the makefile. 
c) Copy the binary file (Prime/Palindrome) to the home directory of user 
yourrollnumbercoimbatore using scp. 
d) Using ssh, log in to yourrollnumbercoimbatore and remotely execute the 
commands for printing the name of current login user and executing the binary 
file (Prime/Palindrome)
