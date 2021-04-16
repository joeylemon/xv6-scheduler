# xv6-scheduler

This is a copy of the [xv6 repository](https://github.com/mit-pdos/xv6-public) which implements a lottery scheduler for processes.

This project was assigned in COSC361 Operating Systems taught by Dr. Micah Beck, as an assignment from the [OSTEP](https://github.com/remzi-arpacidusseau/ostep-projects) textbook.

## Changes to implement feature

### Makefile

- I added the names of the new user programs I created (test, ps) as well as the
new file for utilities (utils.h) to the Makefile so the kernel gets built properly.

### proc.c

- I modified the allocproc() function to initialize processes with 10 tickets and set
their inuse flag and tick count to 0.
- I modified the fork() function to make children processes inherit their parent
process’s ticket count.
- I created a new function named total_lottery_tickets() which sums up the total
assigned tickets for all runnable processes.
- I modified the scheduler() function to choose a winning ticket every loop, run the
process with the winning ticket, update

### proc.h

- I added tickets, ticks, and inuse integer fields to the proc struct.
- I moved the definition of ptable to this header file and exported it so the
sys_getpinfo() syscall could get the list of process information

### ps.c

- I created a user program which uses the getpinfo() syscall to list information
about all processes, similar to ps on Linux.

### pstat.h

- I defined the given pstat struct in this header file.

### spinlock.h

- I added a #ifndef declaration because proc.h was having double declaration
issues with spinlock.

### syscall.c

- I added the declarations for the two new syscalls: sys_settickets() and
sys_getpinfo().

### syscall.h

- I added the definitions for the two new syscall numbers.

### sysproc.c

- I implemented the definitions of the two new syscalls: sys_settickets() and
sys_getpinfo().

### test.c

- I created a user program which forks children with differing ticket counts and
measures their share of CPU ticks. I exported the results to Excel to create a
graph.

<p align="center"><img src="https://user-images.githubusercontent.com/8845512/114961465-0dfce700-9e37-11eb-865e-25651d6ef99d.png" /></p>

### user.h

- I added the user declarations for the two new syscalls: settickets() and
getpinfo().

### usys.S

- I added the user definitions of the two new syscalls: settickets() and getpinfo().

### utils.c

- I created a new file which holds utility functions. It currently holds a random()
function to generate pseudo-random numbers.

### utils.h

- I added the definition of the new random() function.
