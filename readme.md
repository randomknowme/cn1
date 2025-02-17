https://github.com/randomknowme/cn1

https://github.com/randomknowme/cn2

https://github.com/randomknowme/cn3

gpt https://chatgpt.com/c/677ca69b-2d08-8001-be39-58ac8e4fb8fd

# unit 
# producer consumer

The Producer-Consumer Problem is a synchronization issue where a producer adds data to a shared buffer, and a consumer removes data. Race conditions occur if both access the buffer simultaneously without proper synchronization, leading to buffer overflow (when the producer adds too much data) or buffer underflow (when the consumer tries to remove from an empty buffer). Semaphores or mutexes are used to prevent these issues
---
```c
#include <stdio.h>
#include <stdlib.h>

int mutex = 1, full = 0, empty = 3, x = 0;

int wait(int s) { return --s; }
int signal(int s) { return ++s; }

void producer() {
    mutex = wait(mutex);
    empty = wait(empty);
    full = signal(full);
    printf("\nProduced item %d", ++x);
    mutex = signal(mutex);
}

void consumer() {
    mutex = wait(mutex);
    full = wait(full);
    empty = signal(empty);
    printf("\nConsumed item %d", x--);
    mutex = signal(mutex);
}

int main() {
    int choice;
    printf("\n1. Produce\n2. Consume\n3. Exit");
    
    while (1) {
        printf("\nChoice: ");
        scanf("%d", &choice);
        
        if (choice == 1 && mutex == 1 && empty > 0) producer();
        else if (choice == 2 && mutex == 1 && full > 0) consumer();
        else if (choice == 3) exit(0);
        else printf("Invalid or buffer full/empty!");
    }
}
```
---
# fork
A system call that creates a new child process.
Returns 0 to the child, child’s PID to the parent.
```c
#include <stdio.h>
#include <unistd.h>

int main() {
    pid_t pid = fork();

    if (pid < 0) {
        printf("Fork failed!\n");
    }
    else if (pid == 0) {
        printf("Child Process: PID = %d\n", getpid());
        printf("Child Process: Parent PID = %d\n", getppid());
    }
    else { 
        printf("Parent Process: PID = %d\n", getpid());
        printf("Parent Process: Child PID = %d\n", pid);
    }

    return 0;
}

```
# wait
Makes a parent process wait for a child to complete execution.
Helps in process synchronization.
```c
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <sys/wait.h>

int main() {
    pid_t pid = fork();

    if (pid < 0) {
        printf("Fork failed!\n");
        exit(1);
    }
    else if (pid == 0) {
        printf("Child Process: PID = %d\n", getpid());
        printf("Child Process: Parent PID = %d\n", getppid());
        sleep(2);
        printf("Child Process: Exiting now.\n");
        exit(5);
    }
    else {
        int status;
        printf("Parent Process: Waiting for child to complete...\n");
        wait(&status);
        printf("Parent Process: Child exited with status %d\n", WEXITSTATUS(status));
        printf("Parent Process: Resuming execution.\n");
    }

    return 0;
}
```
---
# exec
Replaces the current process image with a new program.
Used in combination with fork().
```c
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <sys/wait.h>

int main() {
    pid_t pid = fork();

    if (pid < 0) {
        printf("Fork failed!\n");
        exit(1);
    }
    else if (pid == 0) {
        printf("Child Process: Executing 'ls -l'\n");
        char *args[] = {"ls", "-l", NULL}; 
        execvp("ls", args);
        perror("exec failed");
        exit(1);
    }
    else {
        wait(NULL);
        printf("Parent Process: Child completed execution.\n");
    }

    return 0;
}
```

---
# sleep
Pauses a process for a specific time (in seconds).
Used to simulate delays.
```c
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>

int main() {
    pid_t pid = fork();

    if (pid == 0) {
        printf("Child Process: PID = %d\n", getpid());
        sleep(5);
        printf("Child Process: Woke up after 5 seconds.\n");
    } else {
        printf("Parent Process: PID = %d\n", getpid());
        sleep(2);
        printf("Parent Process: Woke up after 2 seconds.\n");
    }

    return 0;
}
```
---
# Semaphores implementation with no busy waiting
Uses blocking instead of looping to reduce CPU usage.
Example: wait() and signal() operations block a process until resources are available instead of repeatedly checking.
![WhatsApp Image 2025-02-17 at 23 19 23_1d4ce525](https://github.com/user-attachments/assets/217e87c0-98a3-4391-94b2-0a1283396b95)

---
https://github.com/randomknowme/cn1

https://github.com/randomknowme/cn2

https://github.com/randomknowme/cn3
