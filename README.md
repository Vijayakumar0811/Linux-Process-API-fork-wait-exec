# Linux-Process-API-fork-wait-exec-
Ex02-Linux Process API-fork(), wait(), exec()
# Ex02-OS-Linux-Process API - fork(), wait(), exec()
Operating systems Lab exercise


# AIM:
To write C Program that uses Linux Process API - fork(), wait(), exec()

# DESIGN STEPS:

### Step 1:

Navigate to any Linux environment installed on the system or installed inside a virtual environment like virtual box/vmware or online linux JSLinux (https://bellard.org/jslinux/vm.html?url=alpine-x86.cfg&mem=192) or docker.

### Step 2:

Write the C Program using Linux Process API - fork(), wait(), exec()

### Step 3:

Test the C Program for the desired output. 

# PROGRAM:

## C Program to create new process using Linux API system calls fork() and getpid() , getppid() and to print process ID and parent Process ID using Linux API system calls

```
#include <stdio.h>
#include <unistd.h>
#include <sys/types.h>

int main() {
    pid_t pid;

    // Create a new process
    pid = fork();

    if (pid < 0) {
        // Fork failed
        perror("fork failed");
        return 1;
    } else if (pid == 0) {
        // Child process
        printf("Child Process:\n");
        printf("PID: %d\n", getpid());
        printf("Parent PID: %d\n", getppid());
    } else {
        // Parent process
        printf("Parent Process:\n");
        printf("PID: %d\n", getpid());
        printf("Child PID: %d\n", pid);
    }

    return 0;
}

```









##OUTPUT

<img width="649" height="849" alt="image" src="https://github.com/user-attachments/assets/9c761580-7fea-4a51-b8c7-88f8ac4461c2" />







## C Program to execute Linux system commands using Linux API system calls exec() , exit() , wait() family



```
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <sys/types.h>
#include <sys/wait.h>

int main() {
    pid_t pid;
    int status;

    pid = fork();  // Create a child process

    if (pid < 0) {
        // Fork failed
        perror("fork failed");
        return 1;
    } else if (pid == 0) {
        // Child process

        // Execute the "ls -l" command using execlp()
        printf("Child: Executing 'ls -l'\n");
        execlp("ls", "ls", "-l", (char *)NULL);

        // If execlp returns, it must have failed
        perror("execlp failed");
        exit(EXIT_FAILURE);  // Exit child process with failure
    } else {
        // Parent process
        printf("Parent: Waiting for child to finish...\n");

        // Wait for child process to finish
        wait(&status);

        if (WIFEXITED(status)) {
            printf("Parent: Child exited with status %d\n", WEXITSTATUS(status));
        } else {
            printf("Parent: Child terminated abnormally\n");
        }
    }

    return 0;
}

```





















##OUTPUT

<img width="841" height="948" alt="Screenshot from 2025-10-08 11-48-58" src="https://github.com/user-attachments/assets/ad1674aa-2157-4b3f-ad1f-cdfc968fcb35" />


<img width="841" height="667" alt="image" src="https://github.com/user-attachments/assets/edb7f7ba-506c-46b0-8424-b4f12b82b102" />















# RESULT:
The programs are executed successfully.
