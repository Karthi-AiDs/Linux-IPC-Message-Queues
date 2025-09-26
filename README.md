# Linux-IPC-Message-Queues
Linux IPC-Message Queues

# AIM:
To write a C program that receives a message from message queue and display them

## Name : Karthikeyan D
## Reg No: 212224230115

# DESIGN STEPS:

### Step 1:

Navigate to any Linux environment installed on the system or installed inside a virtual environment like virtual box/vmware or online linux JSLinux (https://bellard.org/jslinux/vm.html?url=alpine-x86.cfg&mem=192) or docker.

### Step 2:

Write the C Program using Linux message queues API 

### Step 3:

Execute the C Program for the desired output. 

# PROGRAM:

## C program that receives a message from message queue and display them
## Writer Side
```
#include <stdio.h> 
#include <sys/ipc.h> 
#include <sys/msg.h> 

// structure for message queue 
struct mesg_buffer { 
	long mesg_type; 
	char mesg_text[100]; 
} message; 
int main() 
{ 	key_t key; 
	int msgid; 
	key = ftok("progfile", 65); 
	msgid = msgget(key, 0666 | IPC_CREAT); 
	message.mesg_type = 1; 
	printf("Write Data : "); 
	fgets(message.mesg_text,sizeof(message.mesg_text),stdin); 
	msgsnd(msgid, &message, sizeof(message), 0);
	
	 
	// display the message 
	printf("Data send is : %s \n", message.mesg_text); 
	return 0; 
} 

```

## Client Server

```
#include <stdio.h>
#include <sys/ipc.h>
#include <sys/msg.h>

// structure for message queue
struct mesg_buffer {
	long mesg_type;
	char mesg_text[100];
} message;
int main()
{
	key_t key;
	int msgid;
	key = ftok("progfile", 65);

	msgid = msgget(key, 0666 | IPC_CREAT);

	msgrcv(msgid, &message, sizeof(message), 1, 0);

	printf("Data Received is : %s \n",
			message.mesg_text);

	// to destroy the message queue
	msgctl(msgid, IPC_RMID, NULL);
	return 0;
}

```

## OUTPUT

<img width="748" height="155" alt="Screenshot from 2025-09-26 09-17-37" src="https://github.com/user-attachments/assets/7ba8ce6d-a959-4983-8ce6-efba9156213a" />

# RESULT:
The programs are executed successfully.
