1) Login as a root user. 

![image](https://user-images.githubusercontent.com/67383098/235846557-b5e6c108-7e3a-4137-a9d8-84e7625227a2.png)


3) Create two users yourrollnumberamrita(client) and yourrollnumbercoimbatore(server) 
with passwords. 

![image](https://user-images.githubusercontent.com/67383098/235847130-f17af453-5fdf-4fa0-82f0-6fc9c7766750.png)


3) Login as yourrollnumberamrita. Use ssh to create the private and public ids at the 
location /home/yourrollnumberamrita/.ssh 

![image](https://user-images.githubusercontent.com/67383098/235847330-490cce8d-b91a-4798-803b-4aec9ea5d4d8.png)

![image](https://user-images.githubusercontent.com/67383098/235847468-10564574-711c-4859-a2c9-93f73e1a1c01.png)


4) Then copy the public id file to the 
/home/yourrollnumbercoimbatore/.ssh/authorized_keys 

![image](https://user-images.githubusercontent.com/67383098/235865538-92fc0657-64ca-4587-87df-2975da1feb3f.png)


5) Do the necessary steps if required (editing ssh config files and restarting the service, 
providing permissions for .ssh and .ssh/ authorized_keys etc..) 

![image](https://user-images.githubusercontent.com/67383098/235865817-6f342318-d3ed-454e-9f4c-59469ad6ab11.png)

![image](https://user-images.githubusercontent.com/67383098/235866192-dc707a69-b99c-4f97-8fad-493f2088934d.png)

![image](https://user-images.githubusercontent.com/67383098/235866236-8c0ec0dc-87aa-4268-91d0-50d321028a06.png)

![image](https://user-images.githubusercontent.com/67383098/235866333-3ba04ead-6efa-46b6-9e01-9a9ec8bfe7e9.png)



6) Check are you able to login without a password from yourrollnumberamrita to 
yourrollnumbercoimbatore using ssh 

Now we can ssh into the server user without a password,

![image](https://user-images.githubusercontent.com/67383098/235865706-d5366f71-eb6f-4d6e-bfe4-925a251b3222.png)

7) Then switch user to yourrollnumberamrita. 

![image](https://user-images.githubusercontent.com/67383098/235866692-0696cf4a-5ff9-4c49-89d1-00ce1710d90c.png)

9) Write a script remoteshell.sh which will do the following sub-tasks 
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


```
#!/bin/bash

echo "The current user is: $(whoami)"

cd /home/amrita22005client   # change to the directory that contains the Makefile
make   # run the make command to build the project

./prime 22005   # run the binary with the input 22005

scp prime cbe22005server:~/   # copy the binary file 'prime' to the home directory of user 'cbe22005server'

ssh cbe22005server "echo 'The current user is: \$(whoami)'; ./prime 22005"  # ssh into the user cbe22005server and run the command to print the current user and run the binary file 'prime' with the input 22005

````



Makefile,

```
CC = gcc
CFLAGS = -c


prime: prime.o
	$(CC) $(LDFLAGS) $^ $(LDLIBS) -o $@

prime.o: prime.c
	$(CC) $(CFLAGS)  $< -o $@

clean:
	$(RM) prime.o prime
```

prime

```
#include <stdio.h>
#include <stdlib.h>

int main(int argc, char *argv[]) {
    int num, i, isPrime = 1;
    if (argc != 2) {
        printf("Usage: %s <number>\n", argv[0]);
        return 1;
    }
    num = atoi(argv[1]);
    if (num <= 1) {
        printf("The number %d is not prime.\n", num);
        return 0;
    }
    for (i = 2; i <= num / 2; ++i) {
        if (num % i == 0) {
            isPrime = 0;
            break;
        }
    }
    if (isPrime)
        printf("The number %d is prime.\n", num);
    else
        printf("The number %d is not prime.\n", num);
    return 0;
}

```

![image](https://user-images.githubusercontent.com/67383098/235875044-a9b57087-58b8-4828-8f44-35417f8944e5.png)


```
# SSH into cbe22005server and print the name of the current user
ssh -t cbe22005server "echo 'Current user: $(whoami)'; echo 'Server name: $HOSTNAME'"

# Run the binary on cbe22005server with the input number
ssh cbe22005server "/home/cbe22005server/prime 22005"

ssh -t cbe22005server "echo 'Current user: $(whoami)'; echo 'Server name: $HOSTNAME'; /home/cbe22005server/prime 22005"
```













