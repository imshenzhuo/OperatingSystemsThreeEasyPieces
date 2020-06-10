### Fork

The newly-created process (called the child, in contrast to the creating parent) doesn’t start running at main()!

### Wait

>  如何让子进程先执行完的

if the parent does happen to run first, it will immediately call wait(); this system call won’t return until
the child has run and exited.

### Exec

- it loads code (and static data) from that executable and overwrites its current code segment (and current static data) with it
- the heap and stack and other parts of the memory space of the program are reinitialized.
- Then the OS simply runs that program

it does not create a new process;
rather, it transforms the currently running program (formerly p3) into a different running program (wc).

## Why API

why `fork & exec` ?

it lets the shell run code *after the call to fork() but before the call to exec()*;

this code can alter the environment of the about-to-be-run program, and thus enables a variety
of interesting features to be readily built.

The shell is just a user program 4 . It shows you a prompt and then
waits for you to type something into it. You then type a command (i.e.,
the name of an executable program, plus any arguments) into it; in most
cases, the shell then figures out where in the file system the executable
resides, calls fork() to create a new child process to run the command,
calls some variant of exec() to run the command, and then waits for the
command to complete by calling wait(). When the child completes, the
shell returns from wait() and prints out a prompt again, ready for your
next command.



