# Linux-IPC-Shared-memory
Ex06-Linux IPC-Shared-memory

# AIM:
To Write a C program that illustrates two processes communicating using shared memory.

# DESIGN STEPS:

### Step 1:

Navigate to any Linux environment installed on the system or installed inside a virtual environment like virtual box/vmware or online linux JSLinux (https://bellard.org/jslinux/vm.html?url=alpine-x86.cfg&mem=192) or docker.

### Step 2:

Write the C Program using Linux Process API - Shared Memory

### Step 3:

Execute the C Program for the desired output. 

# PROGRAM:

## Write a C program that illustrates two processes communicating using shared memory.
```
// shm_writer.c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <sys/ipc.h>
#include <sys/shm.h>
#include <sys/types.h>

int main() {
    key_t key = ftok("/tmp/shmfile", 65);
    if (key == -1) { perror("ftok"); return 1; }

    int shmid = shmget(key, 1024, 0666 | IPC_CREAT);
    if (shmid == -1) { perror("shmget"); return 1; }

    char *data = (char*) shmat(shmid, NULL, 0);
    if (data == (char*) -1) { perror("shmat"); return 1; }

    printf("Shared memory id = %d\n", shmid);
    printf("Type a line and press Enter (this will be written to shared memory):\n> ");
    if (fgets(data, 1024, stdin) == NULL) {
        printf("No input.\n");
    } else {
        printf("Data written in memory: %s", data);
    }

    if (shmdt(data) == -1) perror("shmdt");
    return 0;
}
```




## OUTPUT

<img width="818" height="769" alt="image" src="https://github.com/user-attachments/assets/8cd006bb-dd04-4371-a33f-ac5d31b00526" />

# RESULT:
The program is executed successfully.
