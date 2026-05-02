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

Program:
```
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>

int main() {
    int pid = fork();

    if (pid == 0) { 
        printf("I am child, my PID is %d\n", getpid()); 
        printf("My parent PID is: %d\n", getppid()); 
        sleep(2);  // Keep child alive for verification
    } else { 
        printf("I am parent, my PID is %d\n", getpid()); 
        wait(NULL); 
    }
}
```
<img width="558" height="408" alt="Screenshot 2026-05-02 145552" src="https://github.com/user-attachments/assets/9ec42433-1878-400b-bf19-49f37fa76273" />

##OUTPUT

<img width="300" height="130" alt="Screenshot 2026-05-02 145517" src="https://github.com/user-attachments/assets/59e78128-71a7-496d-bf2e-97f21ad5860f" />

<img width="660" height="124" alt="Screenshot 2026-05-02 152701" src="https://github.com/user-attachments/assets/060e3529-d987-4700-b6bb-a69023025f20" />

## C Program to execute Linux system commands using Linux API system calls exec() , exit() , wait() family

Program:
```
#include <stdio.h>
#include <stdlib.h>
#include <sys/types.h>
#include <sys/wait.h>
#include <unistd.h>

int main() {
    int status;
    
    printf("Running ps with execl\n");
    if (fork() == 0) {
        execl("ps", "ps", "-f", NULL);
        perror("execl failed");
        exit(1);
    }
    wait(&status);
    
    if (WIFEXITED(status)) {
        printf("Child exited with status: %d\n", WEXITSTATUS(status));
    } else {
        printf("Child did not exit successfully\n");
    }
    
    printf("Running ps with execlp (without full path)\n");
    if (fork() == 0) {
        execlp("ps", "ps", "-f", NULL);
        perror("execlp failed");
        exit(1);
    }
    wait(&status);
    
    if (WIFEXITED(status)) {
        printf("Child exited for execlp with status: %d\n", WEXITSTATUS(status));
    } else {
        printf("Child did not exit successfully\n");
    }
    
    printf("Done.\n");
    return 0;
}
```
<img width="915" height="790" alt="Screenshot 2026-05-02 210426" src="https://github.com/user-attachments/assets/c831db73-7c00-43af-b045-2cee1c3a50ab" />


##OUTPUT

<img width="769" height="521" alt="Screenshot 2026-05-02 210531" src="https://github.com/user-attachments/assets/01212a29-1389-4d74-93cd-fb87c6586dc1" />


# RESULT:
The programs are executed successfully.
