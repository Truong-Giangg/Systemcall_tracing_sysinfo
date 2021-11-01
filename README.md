# Systemcall_tracing_sysinfo
--------------------------------------------TRACING----------------------------------------------
This experiment is used to give us an understanding of how to implement the xv6 system call, and then take trace as an example. The specific function is to track the corresponding system call according to the parameters. The code logic is relatively simple, but there are more places to be modified. Below Step by step instructions
a. The first thing to do is to add $U/_trace to the UPROGS variable in the Makefile

b. Then we look at user/trace.c (at first we thought we had to write it by ourselves, but later found that the user mode trace has been written orz), and then found that the trace function of the system call only needs to record a mask.
c. Then because you want to recognize user/trace.c when compiling, you need to add a statement to user/user.h, add an entry to user/usys.pl and a syscall number to kernel/syscall.h, and then you have to implement the function Part of

d. Add sys_trace() to kernel/sysproc.c. It’s best to take a look at how other functions in kernel/sysproc.c get parameters and run. The proc structure in kernel/proc.h needs to be modified (record the current Process information), add a mask value to proc to identify the system number
e. Then after the implementation is completed, modify the fork function in kernel/proc.c to add the function of copying the mask of the parent process by the child process
f. Then the last is to modify kernel/syscall.c, first add the declaration sys_trace function, and then add it to the syscalls array, then modify the syscall function to add trace identification function, complete part1



--------------------------------------------SYSINFO----------------------------------------------
The experimental requirements are relatively simple, to implement a function that can obtain the number of available processes and available memory in the current system, as long as it passes the test given by it.

The first few parts of the experiment are the same as (1)

1. Add $U/_sysinfo
2. Add function declaration to user.h, add entry to usys.pl, add syscall number to syscall.h, and then add it to the syscall function array
3. Then in order to add the sys_sysinfo function to kernel/sysproc.c, in order to achieve this, you need to add functions in kernel/proc.c and kernel/kalloc.c to obtain the process being used and the number of available memory, and then remember to add Function declaration is in defs.h
4. Then implement the sys_sysinfo function, here you need to look at the use of the copyout function (you can refer to sys_fstat (kernel / sysfile.c) and filestat (kernel / file.c))
