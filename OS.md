# Operating Systems

Provide consistent abstractions to applications, even on different hardware

Manage sharing of resources among multiple applications

The key building blocks:

- Processes

- Threads, Concurrency, Scheduling, Coordination

- Address Spaces

- Protection, Isolation, Sharing, Security

- Communication, Protocols

- Persistent storage, transactions, consistency, resilience

- Interfaces to all devices

**Definition of an Operating System**

No universally accepted definition

"Everything a vendor ships when you order an operating system" is good approximation

- But varies wildly

"The one program running at all times on the computer" is the <u>kernel</u>

- Everything else is either a system program (ships with the operating system) or an application program

Special layer of software that provides application software access to hardware resources

- Convenient abstraction of complex hardware devices

- Protected access to shared resources

- Security and authentication

- Communication

System:

- Multiple interrelated parts
  
  - Each potentially interacts with the others

- Robustness requires an engineering mindset
  
  - Meticulous error handling, defending against malicious careless users
  
  - Treating the computer as a concrete machine, with all of its limitations and possible failure cases

The OS abstracts these hardware details from the application

*Provide clean, easy-to-use abstractions of physical resources*

- *Infinite memory, dedicated machine*

- *Higher level objects: files, users, messages*

- *Masking limitations, virtualization*

*Manage protection, isolation, and sharing of resources*

- *Resource allocation and communication*

*Common services*

- *Storage, Window system, Networking*

- *Sharing, Authorization*

- *Look and feel*

Process: Execution environment with restricted rights provided by OS

Application's "machine" is the process abstraction provided by the OS

Each running program runs in its own process

Processes provide nicer interfaces than raw hardware

A process consists of:

- Address Space

- One or more threads of control executing in that address space

- Additional system state associated with it
  
  - Open files
  
  - Open sockets (network connections)

OS translates from hardware interface to application interface

OS provides each running program with its own process

The protection idea is really the os synthesizes a protection boundary which protects the processes running on top of the virtualization from the hardware and prevents those processes from doing things that we've deemed not correct that are not part of the protection.

You as a programmer don't want to think about the about the individual hardware, because if you had to do that, you wouldn't be getting anything done. And so part of what the os does is it really puts these protection boundaries in, gives you a clean virtualization precisely so you can program without thinking about those things.

OS isolates processes from each other.

OS isolates itself from other processes, even though they are actually running on the same hardware.

OS provides common services in the form of I/O

The Windows NT initially had was a microkernel type operating system and the windowing system was outside of the kernel. And then they decided they weren't getting enough performance. And so they went the opposite direction and put the windowing entirely inside of the kernel, which is almost like a reactionary response. And so you could have windowing both in and out of the kernel, and distinctions there have to do with protection, security, durability, reliability.

We got to deal with power management and some of those things which only really show up on portable devices, but these are all potentially managed by the os.

Some of people will actually design and build operating systems or components of them. Many of people will create systems that utilize the core concepts in operating systems. Whether you build software or hardware, the concepts and design patterns appear at many levels. Building applications, etc. that utilize operating systems. The better you understand their design and implementation, the better use you'll make of them.

---

**OS Concepts**: Process, I/O, Networks and Virtual Machines

**Concurrency**: Threads, scheduling, locks, deadlock, scalability, fairness

**Address Space**: Virtual memory, address translation, protection, sharing

**File Systems**: I/O devices, file objects, storage, naming, caching, performance, paging, transactions, databases

**Distributed Systems**: Protocols, N-Tiers, RPC, NFS, DHTs, Consistency, Scalability, multicast

**Reliability & Security**: Fault tolerance, protection, security

**Cloud Infrastructure**

---

**Moore's Law**: Gordon Moore predicted in 1965 that the transistor density of semiconductor chips would double roughly every 18 months.

Microprocessors have become smaller, denser, and more powerful.

Moore's law extrapolation: Potential power density reaching amazing levels.

Parallelism must be exploited at all levels.

Moore's law has (officially) ended -- Feb 2016

- No longer getting 2x transistors/chip every 18 months

- or even every 24 months

May have only 2-3 smallest geometry fabrication plants left:

- Intel and Samsung and/or TSMC

Vendors moving to 3D stacked chips

- More layers in old geometries

In 2011, smartphone shipments exceeded PC shipments.

**Complexity**:

- Applications consisting of
  
  - a variety of software modules that
  
  - run on a variety of devices (machines) that
    
    - implement different hardware architectures
    
    - run competing applications
    
    - fail in unexpected ways
    
    - can be under a variety of attacks

Not feasible to test software for all possible environments and combinations of combinations of components and devices

- The question is not whether there are bugs but how serious are the bugs!

**Operating systems basically help the programmer write robust programs.**

- Provide convenient abstractions to handle diverse hardware
  
  - Convenience, protection, reliability obtained in creating the illusion

- Coordinate resources and protect users from each other
  
  - Using a few critical hardware mechanisms

- Simplify application development by providing standard services

- Provide fault containment, fault tolerance, and fault recovery

OS combines things from many other areas of CS: Languages, data structures, hardware, and algorithms.

---

The core chip itself is directly connected to really high band widdram channels and high speed graphics and so on. And then there is a interface, the direct media interface, to what's often used to be called the South Bridge, but is basically the chip that connects to all the rest of the I/O. And off of that, we can have things like high speed I/O devices for PCI Express. We can have discs. We can have slow I/O through USB. We can have Ethernet, HD Audio, PCIe drives, RAID smart connect, whatever. And then there's an even slow interface off of that that gives us BIOS and all sorts of interesting things.

The reason that operating systems are so crucial is they provide a way to take this complexity and manage it.

There are millions of lines of code for different things that you're familiar with.

New Versions usually (much) larger older versions.

Cars getting really complex. There is almost 100 million lines of code in a modern car.

Third-party device drivers are one of the most unreliable aspects of OS

- Poorly written by non-stake-holders

- Ironically, the attempt to provide clean abstractions can lead to crashes!

Holes in security model or bugs in OS lead to instability and privacy breaches.

- Great Example: Meltdown (2017)
  
  - Extract data from protected kernel space!

Version skew on Libraries can lead to problems with application execution.

Data breaches, DDOS attacks, timing channels...

- Heartbleed (SSL)

The operating system is really trying to help abstract the underlying hardware and tame complexity.

You could think of there's hardware underneath the operating system is in between to provide a clean abstraction, which we'll will even call a virtual machine abstraction to the operating system.

If you actually look at people that have measured the root causes of a lot of crashes, something upwards of 50 or 60% of crashes at one point in time were actually attributable to bugs in device drivers, which is pretty spectacular.

- Processor → Thread

- Memory → Address Space

- Disks, SSDs, ... → Files

- Networks → Sockets

- Machines → Processes

| Application                         |
|:-----------------------------------:|
| *<u>Abstract Machine Interface</u>* |
| **Operating System**                |
| *<u>Physical Machine Interface</u>* |
| **Hardware**                        |

The BIOS is typically a way of providing a set of standardized services on top of hardware. And part of the BIOS is a legacy to old days in the IBM CS. But some of it also provides firmware that can get updated and help the hardware be a little bit more reliable, thereby making the operating system job better.

Device drivers run in supervisor mode, which is one of the reasons except for microkernels.

Oftentimes, the hardware interface talks about a set of mechanisms that the operating system exploits to provide a set of clean mechanisms and policies up to software.

FOUR FUNDAMENTAL OS CONCEPTS:

- **Thread: Execution Context**
  
  - Fully describes program state
  
  - Program Counter, Registers, Execution Flags, Stack

- **Address Space** (with or w/o **translation**)
  
  - Set of memory addresses accessible to program (for read or write)
  
  - May be distinct from memory space of the physical machine
    
    (in which case programs operate in a virtual address space)

- Process: an instance of a running program
  
  - Protected Address Space + One or more Threads

- Dual mode operation / Protection
  
  - Only the "system" has the ability to access certain resources
  
  - Combined with translation, isolates programs from each other and the OS from programs

Dual mode operation, which is the fact that a typical processor has at least two different modes. Which we may loosely call kernel mode and user mode. And we exploit that to give us our better virtual machine behavior.

**OS Bottom Line: Run Programs**

- Write them and compile them

- Load instruction and data segments of executable file into memory

- Create stack and heap

- "Transfer control to program"

- Provide services to program

- While protecting OS and program

The processor was something that started out with having a program counter, and a memory that it could read. And in that memory was a set of instructions. And so that program counter would point into the memory and allow the processor to fetch the next instruction. So we pull the instruction in from memory, we would decode it. And then we would feed it to the execution pipeline, which is a five stage execution pipeline for a risk style processor. And after things were decoded, they would feed a set of registers and an ALU to do actual operations and execute as desired and at that point, you go on to the next instruction and so on and increment the program counter.

**First OS Concept: Thread of Control**

A thread is really a single unique execution context. And it's got a program counter registers, execution, plague stack, memory state.

A very simple fetch execute cycle, once we get to something we want to provide to other people, to users in particular, we need to virtualize it. And so the thread is going to be like a virtualized version of processor.

A thread is **executing** on a processor (core) when it is **resident** in the processor registers.

*We may have many threads, but on a given core, only one of them is resident and has control of the program counter and registers at any given time.*

Resident means: Registers hold the root state (context) of the thread:

- Including program counter (PC) register & currently executing instruction
  
  - PC points at next instruction **in memory**
  
  - **Instructions stored in memory**

- Including intermediate values for ongoing computations
  
  - Can include actual values (like integers) or pointers to values **in memory**

- Stack pointer holds the address of the top of stack (which is **in memory**)

- **The rest is "in memory"**

*Once you get into pipelining, which you started to learn about it, there's a lot of pipeline state involved in an ongoing execution.*

A thread is suspended (not executing) when its state **is not** loaded (resident) into the processor

- Processor state pointing at some other thread

- Program counter register **is not** pointing at next instruction from this thread

- Often: a copy of the last value for each register stored in memory

Execution sequence:

- Fetch Instruction at PC

- Decode

- Execute (possibly using registers)

- Write results to registers/mem

- PC = Next Instruction (PC)

- Repeat

If you check the Task Manager on your laptop, you'll find that there are hundreds of processes that are just running, mostly sleeping, but they're all available on your current processor. 

Let's mostly assume that a physical processor has only one core on it or one freread of execution in the hardware at any given time. We've got here is we want to have the illusion of multiple CPU's running at the same time. So we can have multiple threads running at the same time. We're going to have them all share the same memory so that the programmerers view as well. Just have a bunch of things running and they all share memory.

We're going to multiplex that hardware in time. So threads are **virtual cores**.

$vCPU_1$ → $vCPU_2$ → $vCPU_3$ → $vCPU_1$ → $vCPU_2$ → ...

We repeat and so over time,  and we get this multiplexing of the same physical hardware.

Contents of virtual core (thread):

- Program counter, stack pointer

- Registers

Where is the thread:

- On the real (physical) core, or

- Saved in chunk of memory - called the Thread Control Block (TCB)

What happened:

- OS Ran

- Saved $PC$, $SP$, ... in $vCPU_1$'s thread control block (memory)

- Loaded $PC$, $SP$, ... from $vCPU_2$'s $TCB$, jumped to $PC$

What triggered this switch:

- Timer, voluntary yield, I/O, other things we will discuss

*This can take something of the order of a few microseconds and you wanna make sure that the time to switch isn't so long that you're spending most of your time switching.*

Typically there's one cache per core and so thery're all kind of sharing the same cache. If you switch too quickly, then nobody gets advantage of the cache. The cache or the TLB in a primitive processor has to be flushed, but when you switch more advanced ones, it doesn't.

The cache itself is typically in physical space, and you're switching from one thread to another. You just change page tables. And so you don't actually have to flush the cache.

The question about how many registers there are is going to depend vastly on which processor you've got. There are 32 integer registers on a RISC-V and there are some floating point one as well. On an x86, there's a much smaller number of registers, and so when you don't have registers in the processor, you got to keep things in memory, so you spend a lot of time going back and forth.

Thread Control Block (TCB)

- Holds contents of registers when thread not running

- TCBs stored in the kernel

**Second OS Concept: Address Space**

Address space → the set of accessible addresses + state associated with them:

- For 32-bit processor: $2^{32}$ = 4 billion ($10^9$) addresses

- For 64-bit processor: $2^{64}$ = 18 quadrillion ($10^{18}$) addresses

| stack           | 0xFFF...     |
|:---------------:| ------------ |
| ↓↑              |              |
| **heap**        |              |
| **Static Data** |              |
| **code**        | **0x000...** |

What happens when you read or write to an address

- Perhaps acts like regular memory

- Perhaps ignores writes

- Perhaps causes I/O operation
  
  (Memory-mapped I/O)

- Perhaps causes exception (fault)

- Communicates with another program

- ...

All vCPU's share non-CPU resources

- Memory, I/O Devices

Each thread can read/write memory

- Perhaps data of others

This approach is used in

- Very early days of computing

- Embedded applications

- MacOS 1-9 / Windows 3.1 (switch only with voluntary yield)

- Windows 95-ME (switch with yield or timer)

However, it is risky. You work on windows 31 systems where you put the wrong application in there and all of a sudden, everything locked up. That's rather undesirable, no protection.

Simple Multiplexing has no protection!

Operating System must protect itself from user programs

- Reliability: compromising the operating system generally causes it to crash

- Security: limit the scope of what threads can do

- Privacy: limit each thread to the data it is permitted to access

- Fairness: each thread should be limited to its appropriate share of system resources (CPU time, memory, I/O, etc)

OS must protect User programs from one another

- Prevent threads owned by one user from impacting threads owned by another user

- Example: prevent one user from stealing secret information from another user

Simple Protection: Base and Bound (B&B)

- Still protects OS and isolates program

- Requires relocating loader

- No addition on address path

A lot of early systems did relocation, and had some base in bound possibilities to work.

Relocation:

- Compiled .obj file linked together in an .exe

- All address in the .exe are as if it were loaded at memory address 00000000

- File contains a list of all the addresses that need to be adjusted when it is "relocated" to somewhere else.

Address Space Translation:

- Program operates in an address space that is distinct from the physical memory space of the machine

Paged Virtual Address Space:

- All pages same size, so easy to place each page in memory!

- Hardware translates address using a page table
  
  - Each page has a separate base
  
  - The "bound" is the page size
  
  - Special hardware register stores pointer to page table
  
  - Treat memory as page size frames and put any page into any frame ...

Paged Virtual Address:

- Instruction operate on virtual addresses
  
  - Instruction address, load/store data address

- Translated to a physical address through a Page Table by the hardware

- Any Page of address space can be in any (page sized) frame in memory
  
  - Or not-present (access generates a page fault)

- Special register holds page table base address (of the process)

**Third OS Concept: Process**

Definition: execution environment with Restricted Rights

- (Protected) Address Space with One or More Threads

- Owns memory (address space)

- Owns file descriptors, file system context, ...

- Encapsulate one or more threads sharing process resources

Application program executes as a process

- Complex applications can fork/exec child processes

Why processes

- Protected from each other

- OS Protected from them

- Processes provides memory protection

Fundamental tradeoff between protection and efficiency

- Communication easier *within* a process

- Communication harder *between* processes

The idea of a protected chunk of memory that's owned exclusively by an entity in an OS, that's called a process. The process has an execution environment with restricted rights and one or more threats.

**Single and Multithreaded Processes**

- Threads encapsulate ***concurrency***:
  
  - "Active" component

- Address spaces encapsulate ***protection***:
  
  - "Passive" component
  
  - Keeps buggy programs from crashing the system

Why have multiple threads per address space?

- Parallelism: take advantage of actual hardware parallelism (e.g. multicore)

- Concurrency: ease of handling I/O and other simultaneous events

**Protection and Isolation**

Why Do We Need Processes

- Reliability: bugs can only overwrite memory of process they are in

- Security and privacy: malicious or compromised process can't read or write other process' data

- (to some degree) Fairness: enforce shares of disk, CPU

Mechanisms:

- Address translation: address space only contains its own data

- Hardware must support **privilege levels**

**Fourth OS Concept: Dual Mode Operation**

***Hardware*** provides at least two modes (at least 1 mode bit):

- ***Kernel Mode*** (or "supervisor" mode)

- ***User Mode***

Certain operations are ***prohibited*** when running in user mode

- Changing the page table pointer, disabling interrupts, interacting directly hardware, writing to kernel memory

- Carefully controlled transitions between user mode and kernel mode
  
  - System calls, interrupts, exceptions

**Additional Layers of Protection for Modern Systems**

- Additional layers of protection through virtual machines or containers
  
  - Run a complete operating system in a virtual machine
  
  - Package all the libraries associated with an app into a container for execution

**3 types of User → Kernel Mode Transfer**

- Syscall
  
  - Process requests a system service, e.g., exit
  
  - Like a function call, but "outside" the process
  
  - Does not have the address of the system function to call
  
  - Like a Remote Procedure Call (RPC)
  
  - Marshall the syscall id and args in registers and exec syscall

- Interrupt
  
  - External asynchronous event triggers context switch
  
  - e.g., Timer, I/O device
  
  - Independent of user process

- Trap or Exception
  
  - Internal synchronous event in process triggers context switch
  
  - e.g., Protection violation (segmentation fault), Divide by zero, ...

All 3 are an UNPROGRAMMED CONTROL TRANSFER

We have the basic mechanism to

- switch between user processes and the kernel,

- the kernel can switch among user processes,

- Protect OS from user processes and processes from each other

**Process Control Block**

Kernel represents each process as a process control block (PCB)

- Status (running, ready, blocked, ...)

- Register state (when not ready)

- Process ID (PID), User, Executable, Priority, ...

- Execution time, ...

- Memory space, translation, ...

Kernel Scheduler maintains a data structure containing the PCBs.

---

**What Threads Are**

Definition from before: *A single unique execution context*

- Describes its representation

It provides the abstraction of: *A single execution sequence that represents a separately schedulable task*

- Also a valid definition!

Threads are a mechanism for concurrency (overlapping execution)

- However, they can also run in parallel (simultaneous execution)

Protection is an orthogonal concept

- A protection domain can contain one thread or many

**Motivation for Threads**

Operating systems must handle multiple things at once (MTAO)

- Processes, interrupts, background system maintenance

Networked servers must handle MTAO

- Multiple connections handled simultaneously

Parallel programs must handle MTAO

- To achieve better performance

Programs with user interface often must handle MTAO

- To achieve user responsiveness while doing computation

Network and disk bound programs must handle MTAO

- To hide network/disk latency

- Sequence steps in access or communication

**Multiprocessing vs. Multiprogramming**

Some Definitions:

- Multiprocessing: Multiple CPUs (cores)

- Multiprogramming: Multiple jobs / processes

- Multithreading: Multiple threads / processes

What does it mean to run two threads concurrently

- Scheduler is free to run threads in any order and interleaving

- Thread may run to completion or time-slice in big chunks or small chunks

**Concurrency is not Parallelism**

Concurrency is about handling multiple things at once (MTAO)

Parallelism is about doing multiple things *simultaneously*

Each thread handles or manages a separate thing or task...

But those tasks are not necessarily executing simultaneously

**Threads Mask I/O Latency**

- A thread is in one of the following three states:
  
  - RUNNING - running
  
  - READY - eligible to run, but not currently running
  
  - BLOCKED - ineligible to run

- If a thread is waiting for an I/O to finish, the OS marks it as BLOCKED

- Once the I/O finally finishes, the OS marks it as READY

**Multithreaded Programs**

- You know how to compile a C program and run the executable
  
  - This creates a process that is executing that program

- Initially, this new process has *one thread* in its own address space
  
  - With code, globals, etc. as specified in the executable

- Q: How can we make a multithreaded process?

- A: Once the process starts, it issues system calls to create new threads
  
  - These new threads are part of the process: they share its address space

**System Calls ("Syscalls")**

If you look at an operating system, we've got this narrow waste idea or the hourglass kind of design where the difference between user and system is at the system call interface. The operating system libraries issue system calls, language run times issue system calls. And so in many cases, the system calls are actually hidden below your programming interface.

In general, Windows and UNIX and OS/2 and iOS and all these different operating systems have different systems called interfaces. But there are at least one set of attempts to standardize. There's a so called POSIX interface, and the POSX system called interface is shared at least partially across a bunch of different operating systems.

**OS Library API for Threads: pthreads**

```c
int pthread_create(pthread_t *thread, const pthread_attr_t *attr,
            void *(*start_routine)(void*), void *arg);
```

- thread is created executing start_routine with arg as its sole argument

- return is implicit call to pthread_exit

```c
void pthread_exit(void *value_ptr);
```

- terminates the thread and makes value_ptr available to any successful join

```c
int pthread_join(pthread_t thread, void **value_ptr);
```

- suspends execution of the calling thread until the target thread terminates

- On return with a non-NULL value_ptr the value passed to pthread_exit() by the terminating thread is made available in the location referenced by value_ptr.

Remember that we're calling system calls and we're hiding it in many cases from users, since we don't want regular users to have to worry about system calls.

```
Library:
    int pthread_create(...){
        Do some work like a normal fn...

        asm code ... syscall # into %eax
        put args into registers %ebx, ...
        special trap instruction

        get return values from regs
        Do some more work like a normal fn...
};
```

```
Kernel:
    get args from regs
    dispatch to system func
    Do the work to spawn the new thread
    Store return value in %eax
```

*pthread_create* is really a special type of function, not written entirely in C, that does some work like a normal function and then has some special assembly in it that sets up the registers in a way the kernel is gonna to recognize. And then it executes a special trap instruction, which is really a way of jumping into the kernel. The kerel says it's a system call. and by jumping into the kernel this way, what we've done is we've transitioned out of user mode into kernel mode because it's an exception. And then that place we jump to very carefully figures out what system call you want. We jump into the kernel, and the kernel knows that this is the create system call for a thread, and it gets the arguments, it does the creation of the thread, and then it returns in that point. There's special place to store the return value. And then it returns, which takes us back to user mode and the bottom of this function, which grabs the return values and then returns like a normal function. So this function isn't the normal function. This is a wrapper around a system call. But as far as the user is concerned, it looks like a function and you've just linked it.

A system call can take a thousand cycles. It depends a lot on what it's doing. And also, you have to save and restore a bunch of registers when you go into the kernel and come out again. Doing system calls is not cheap. This transition from user mode to kernel mode is more than just setting that bit.

When you create threads, what you're doing is you're basically creating, at least initially here, a scheduable entity. And in that instance, multiple things can be running.

**Fork-Join Pattern**

- Main thread creates (forks) collection of sub-threads passing them args to work on...

- ... and then joins with them, collecting results.

**Thread State**

- State shared by all threads in process/address space
  
  - Content of memory (global variables, heap)
  
  - I/O state (file descriptors, network connections, etc)

- State "private" to each thread
  
  - Kept in $\text{TCB}\equiv \text{Thread Control Block}$
  
  - CPU registers (including, program counter)
  
  - Execution stack

- Execution Stack
  
  - Parameters, temporary variables
  
  - Return PCs are kept while called procedures are executing

**Shared vs. Per-Thread State**

| Shared State     |
|:----------------:|
| Heap             |
| Global Variables |
| Code             |

| Per-Thread State           |
|:--------------------------:|
| Thread Control Block (TCB) |
| Stack Information          |
| Saved Registers            |
| Thread Metadata            |
| Stack                      |

| Per-Thread State           |
|:--------------------------:|
| Thread Control Block (TCB) |
| Stack Information          |
| Saved Registers            |
| Thread Metadata            |
| Stack                      |

**Thread Abstraction**

- Illusion: Infinite number of processors

- Reality: Threads execute with variable "speed"
  
  - Programs must be designed to work with any schedule

A programmer's abstraction is one of lots of threads all running kind of at the same time. An infinite number of processors, whereas the reality is some of them run and some of them don't, and it alternates. So that runs correctly despite the schedulers interleaving.

Proper locking discipline will take care of you here and make sure that you run correctly under all interleavings.

**Correctness with Concurrent Threads**

- Non-determinism:
  
  - Scheduler can run threads in any order
  
  - Scheduler can switch threads at any time
  
  - This can make testing very difficult

- Independent Threads
  
  - No state shared with other threads
  
  - Deterministic, reproducible conditions

- Cooperating Threads
  
  - Shared state between multiple threads

**Shared Data Structure**

Threads can't share stacks. 

The stack represents the current state of an execution. And if you had two threads on the same stack, they just screw each other up and lose.

Each thread has to have its own stack.

- Synchronization: Coordination among threads, usually regarding shared data

- Mutual Exclusion: Ensuring only one thread does a particular thing at a time (one thread excludes the others)
  
  - Type of synchronization

- Critical Section: Code exactly one thread can execute at once
  
  - Result of mutual exclusion

- Lock: An object only one thread can hold at a time
  
  - Provides mutual exclusion

**Locks**

Locks provide two atomic operations:

- Lock.acquire() - wait until lock is free; then mark it as busy
  
  - After this returns, we say the calling thread *holds* the lock

- Lock.release() - mark lock as free
  
  - Should only be called by a thread that currently holds the lock
  
  - After this returns, the calling thread no longer holds the lock

**Bootstrapping**

First process is started by the kernel

- Often configured as an argument to the kernel before the kernel boots

- Often called the "init" process

After this, all processes on the system are created by other processes

**Process Management API**

- exit - terminate a process

- fork - copy the current process

- exec - change the program being run by the current process

- wait - wait for a process to finish

- kill - send a signal (interrupt-like notification) to another process

- sigaction - set handlers for signals

---

**Semaphores**

Semaphores are a kind of generalized lock

- First defined by Dijkstra in late 60s

- Main synchronization primitive used in original UNIX (& Pintos)

Definition: a Semaphore has a non-negative integer value and supports the following two operations:

- P() or down(): atomic operation that waits for semaphore to become positive, then decrements it by 1

- V() or up(): an atomic operation that increments the semaphore by 1, waking up a waiting P, if any

P() stands for "proberen" (to test) and V() stands for "verhogen" (to increment) in Dutch, which is Dijkstra's influence on this.

**Two Semaphore Patterns**

Mutual Exclusion: (like lock)

- Called a "binary semaphore" or "mutex"
  
  ```
  initial value of semaphore = 1;
  semaphore.down();
      // Critical section goes here
  semaphore.up();
  ```

- Signaling other threads, e.g. ThreadJoin
  
  ```
  Initial value of semaphore = 0
  ThreadJoin {
      semaphore.down();
  }
  ```

**System Structure**

Basically, the things that you're used to at the user level all kind of float in the standard libraries, and they're pretty much above the system call interface.

Like an hourglass, the system call interface is the narrow waist, user code runs above, and system code runs below, and then there's a hardware. System call interface is basically a set of standardized functions that you can call that go across users, kernel interfaces. And we're mostly focusing at the os library and above what you do with that.

**pthread**

- pthread library: POSIX thread library

- POSIX: <u>P</u>ortable <u>O</u>perating <u>S</u>ystem <u>I</u>nterface (for uni<u>X</u>?)
  
  - Interface for application programmers (mostly)
  
  - Defines the term "Unix", derived from AT&T Unix
  
  - Created to bring order to many Unix-derived OSes, so applications are portable
    
    - Partially available on non-Unix OSes, like Windows
  
  - Requires standard system call interface

**Unix/POSIX Idea: Everything is a "File"**

This was actually a little bit of a strange idea when it first came out, and now pretty much everybody's used to it, but there's an identical interface for files, for devices like terminals and printers, for networking sockets, for interprocess communication like pipes, etc. All use the same interface with the kernel.

- Identical interface for:
  
  - Files on disk
  
  - Devices (terminals, printers, etc.)
  
  - Regular files on disk
  
  - Networking (sockets)
  
  - Local interprocess communication (pipes, sockets)

- Based on the system calls open(), read(), write(), and close()
  
  - You use those on everything from files on disk to devices, etc.

- Additional: ioctl() for custom configuration that doesn't quite fit

- Note that the "Everything is a File" idea was a radical idea when proposed
  
  - Dennis Ritchie and Ken Thompson described this idea in their seminal paper on UNIX called "The UNIX Time-Sharing System" from 1974

**The File System Abstraction**

- File
  
  - Named collection of data in a file system
  
  - POSIX File data: sequence of bytes
    
    - Could be text, binary, serialized objects, ...
  
  - File Metadata: information about the file
    
    - Size, Modification Time, Owner, Security info, Access control

- Directory
  
  - "Folder" containing files & directories
  
  - Hierachical (graphical) naming
    
    - Path through the directory graph
    
    - Uniquely identifies a file or directory
  
  - Links and Volumes

**Connecting Processes, File Systems, and Users**

- Every process has a current working directory (CWD)
  
  - Can be set with system call:
    
    ```c
    int chdir(const char *path); // change CWD
    ```

- Absolute paths ignore CWD

- Relative paths are relative to CWD

**C High-Level File API - Streams**

Operates on "streams" - unformatted sequences of bytes (wither text or binary data), with a position:

```
#include <stdio.h>
FILE *fopen(const char *filename, const char *mode);
int fclose(FILE *fp);
```

Open stream represented by pointer to a FILE data structure

- Error reported by returning a NULL pointer

**C API Standard Streams - stdio.h**

- Three predefined streams are opened implicitly when the program is executed.
  
  - `FILE *stdin` - normal source of input, can be redirected
  
  - `FILE *stdout` - normal source of output, can too
  
  - `FILE *stderr` - diagnostics and errors

- STDIN / STDOUT enable composition in Unix

- All can be redirected

**C High-Level File API**

```c
// character oriented
int fputc(int c, FILE *fp);    // rtn c or EOF on err
int fputs(const char *s, FILE *fp); // rtn > 0 or EOF

int fgetc(FILE *fp);
char *fgets(char *buf, int n, FILE *fp);

// block oriented
size_t fread(void *ptr, size_t size_of_element,
        size_t number_of_elements, FILE *a_file);
size_t fwrite(const void *ptr, size_t size_of_elements,
        size_t number_of_elements, FILE *a_file);

// formatted
int fprintf(FILE *restrict stream, const char *restrict format, ...);
int fscanf(FILE *restrict stream, const char *restrict format, ...);
```

**C Streams: Char-by-Char I/O**

```c
int main(void) {
    FILE* input = fopen("input.txt", "r");
    FILE* output = fopen("output.txt", "w");
    int c;

    c = fgetc(input);
    while(c!=EOF){
        fputc(output, c);
        c = fgetc(input);
    }
    fclose(input);
    fclose(output);
}
```

**C Streams: Block-by-Block I/O**

```c
#define BUFFER_SIZE 1024
int main(void) {
    FILE* input = fopen("input.txt", "r");
    FILE* output = fopen("output.txt", "w");
    char buffer[BUFFER_SIZE];
    size_t length;
    length = fread(buffer, BUFFER_SIZE, sizeof(char), input);
    while(length > 0){
        fwrite(buffer, length, sizeof(char), input);
        length = fread(buffer, BUFFER_SIZE, sizeof(char), input);
    }
    fclose(input);
    fclose(output);
}
```

**Aside: System Programming**

- Systems programmers should always be paranoid!
  
  - Otherwise you get intermittently buggy code

- We should really be writing things like:
  
  ```c
  FILE* input = fopen("input.txt", "r");
  if(input == NULL) {
      // Prints our string and error msg.
      perror("Failed to open input file")
  }
  ```

- Be thorough about checking return values!
  
  - Want failures to be systematically caught and dealt with

**C High-Level File API: Positioning The Pointer**

```c
int fseek(FILE *stream, long int offset, int whence);
long int ftell(FILE *stream)
void rewind(FILE *stream)
```

For fseek(), the offset is interpreted based on the whence argument (constants in stdio.h):

- `SEEK_SET`: Then offset interpreted from beginning (position 0)

- `SEEK_END`: Then offset interpreted backwards from end of file

- `SEEK_CUR`: Then offset interpreted from current position

**Key Unix I/O Design Concepts**

- Uniformity - everything is a file
  
  - file operations, device I/O, and interprocess communication through open, read/write, close
  
  - Allows simple composition of programs
    
    \>> find | grep | wc ...

- Open before use
  
  - Provides opportunity for access control and arbitration
  
  - Sets up the underlying machinery, i.e., data structures

- Byte-oriented
  
  - Even if blocks are transferred, addressing is in bytes

- Kernel buffered reads
  
  - Streaming and block devices looks the same, read blocks yielding processor to other task

- Kernel buffered writes
  
  - Completion of out-going transfer decoupled from the application, allowing it to continue.

**Low-Level File I/O: The RAW system-call interface**

```c
#include <fcntl.h>
#include <unistd.h>
#include <sys/types.h>

int open(const char *filename, int flags [, mode_t mode])
int creat(const char *filename, mode_t mode)
int close(int filedes)
```

int flags:

```
Bit vector of:
Access modes (Rd, Wr, ...)
Open Flags (Create, ...)
Operating modes (Appends, ...)
```

mode_t mode:

```
Bit vector of Permission Bits:
User|Group|Other X R|W|X
```

- Integer return from open() is a file descriptor
  
  - Error indicated by return < 0: the global errno variable set with error (see man pages)

- Operations on file descriptors:
  
  - Open system call created an open file description entry in system-wide table of open files
  
  - Open file description object in the kernel represents an instance of an open file

**C Low-Level (pre-opened) Standard Descriptors**

```c
#include <unistd.h>
STDIN_FILENO - macro has value 0
STDOUT_FILENO - macro has value 1
STDERR_FILENO - macro has value 2

// Get file descriptor inside FILE *
int fileno(FILE *stream)

// Make FILE * from descriptor
FILE * fdopen(int filedes, const char *opentype)
```

**Low-Level File API**

- Read data from open file using file descriptor:
  
  ```c
  ssize_t read (int filedes, void *buffer, size_t maxsize)
  ```
  
  - Reads up to maxsize bytes - might actually read less!
  
  - returns bytes read, 0 => EOF, -1 => error

- Write data to open file using file descriptor
  
  ```c
  ssize_t write (int filedes, const void *buffer, size_t size)
  ```
  
  - returns number of bytes written

- Reposition file offset within kernel (this is independent of any position held by high-level FILE descriptor for this file)
  
  ```c
  off_t lseek (int filedes, off_t offset, int whence)
  ```

**Low-Level I/O: Other Operations**

- Operations specific to terminals, devices, networking, ...
  
  - e.g., ioctl

- Duplicating descriptors
  
  ```c
  int dup2(int old, int new);
  ```
  
  ```c
  int dup(int old);
  ```

- Pipes - channel
  
  ```c
  int pipe(int pipefd[2]);
  ```
  
  ```
  Writes to pipefd[1] can be read from pipefd[0]
  ```

- File Locking

- Memory-Mapping Files

**State Maintained by the Kernel**

On a successful call to open():

- A file descriptor (int) is returned to the user

- An open file description is created in the kernel

For each process, kernel maintains mapping from file descriptor to open file description

- On future system calls (e.g., read()), kernel looks up open file description using file descriptor and uses it to service the system call:
  
  ```c
  char buffer1[100];
  char buffer2[100];
  int fd = open("foo.txt", O_RDONLY);
  read(fd, buffer1, 100);
  /*
  The kernel remembers that the int it receives
   (stored in fd) corresponds to foo.txt
  */
  read(fd, buffer2, 100);
  ```

---

**Web Server**

The Standard 3 layers:

| Server Process |
|:--------------:|
| **Kernel**     |
| **Hardware**   |

Notice that even a server is running at user level.

All of the kernel code that's giving the glue and the virtual machine and so on is all done in the kernel.

The hardware, of CORS, has got things like networking and disk and so on.

The server process starts up, and the first thing it does is it's gonna to open some sockets to get ready to listen to incoming requests. The first thing it does is a read, and that read goes to the socket and has to take a system call to do that. And the first thing that happens is wait, because there's no data yet. So that server gets put to sleep or the thread that did this gets put to sleep. A server could be multithreaded.

Because there's no data, and notice we've used read. So we're actually going to be communicating with the network in the same way that we did with the file system.

And sometime later, data is going to come in from remotely over the network. And for instance, this might be a request to the web server for reading a certain URL, and it generates an interrupt. It copies things into the socket buffer and then the wait condition is no longer going to be and we're gonna to be able to wake up and remove ourselves from the kernel and basically return from read. So we went into the kernel with read, but we stayed there for a while and then eventually we returned from read with data. And so there's a request.

Now the request, since we're done by a web server, is likely to need to get something off the disk. So it executes a read to a file descriptor for the disk file system. And now it's going to wait a little bit because potentially the disk has to be accessed with the device driver. So that may take some time to pull things off the disk. And then the disk interface will eventually hand back the requested data, which again will remove the weight condition and return from the read system call with data. 

At which point we format the reply like an HTTP reply. We go back to our network socket with a right and that again is a syscall boundary, which will send the packet outgoing and notice that we don't have a weight condition here because we're assuming that the buffers aren't full and the data just goes out. After twelve, we're gonna to just repeat and do another read.

**Communication Between Processes**

Producer (writer) and consumer (reader) may be distinct processes

- Potentially separated in time

Simple option: use a file

When a parent process creates a child process, they share the file descriptor table. And so if you have a file that's been open for reading and writing, and then you produce a child process, then the two of you can exchange data through the disc.

Very expensive if you only want transient communication (non-persistent)

**Communication Between Processes (Another Option)**

- Consider an in-memory queue

- Accessed via system calls (for security reasons)

Data written by A is held in memory until B reads it

- Same interface as we use for files

- Internally more efficient, since nothing goes to disk

**POSIX/Unix PIPE**

Process A:

```c
write(wfd, wbuf, wlen);
```

Process B:

```c
n = read(rfd, rbuf, rmax);
```

Memory Buffer is finite:

- If producer (A) tries to write when buffer full, it blocks (Put sleep until space)

- If consumer (B) tries to read when buffer empty, it blocks (Put to sleep until data)

int pipe(int fileds[2]);

- Allocates two new file descriptors in the process

- Writes to fileds[1] read from fileds[0]

- Implemented as a fixed-size queue

**Protocol**

Once we have communication, we need a protocol

- A protocol is an agreement on how to communicate

- Includes
  
  - Syntax: how a communication is specified & structured
    
    - Format, order messages are sent and received
  
  - Semantics: what a communication means
    
    - Actions taken when transmitting, receiving, or when a timer expires

- Described formally by a state machine
  
  - Often represented as a message transaction diagram

- In fact, across network may need a way to translate between different representations for numbers, strings, etc
  
  - Such translation typically part of a Remote Procedure Call (RPC) facility

**Client-Server Protocols: Cross-Network IPC**

- Many clients accessing a common server

- File servers, www, FTP, databases

You could have one server serving a whole large number of clients and many clients accessing a common server.

Client is "sometimes on"

- Sends the server requests for services when interested
  
  e.g., Web browser on laptop/phone

- Doesn't communicate directly with other clients

- Needs to know server's address

Server is "always on"

- Services requests from many clients
  
  e.g., Web server for www.cnn.com

- Doesn't initiate contact with clients

- Needs a fixed, well-known address

**Network Connection**

Bidirectional stream of bytes between two processes on possibly different machines

Abstractly, a connection between two endpoints A and B consists of:

- A queue (bounded buffer) for data sent from A to B

- A queue (bounded buffer) for data sent from B to A

**The Socket Abstraction: Endpoint for Communication**

Key Idea: Communication across the world looks like File I/O

Sockets: Endpoint for Communication

- Queues to temporarily hold results

Connection: Two Sockets Connected Over the network => IPC over network

There are lots of different types of sockets, but it's not all pipes are sockets. There are ways to get things like pipes that don't have sockets internally and there's also ways of connecting sockets, internally that act like pipes.

The native pipe implementation is actually not the socket implementation on a lot of Unix distributions.

**Sockets: More Details**

***Socket***: An abstraction for one endpoint of a network connection

- Another mechanism for ***inter-process communication***

- Most operating systems (Linux, Mac OS X, Windows) provide this, even if they don't copy rest of UNIX I/O

- Standardized by POSIX

First introduced in 4.2 BSD (Berkeley Standard Distribution) Unix

- This release had some huge benefits (and excitement from potential users)

- Runners waiting at release time to get release on tape and take to businesses

Same abstraction for any kind of network

- Local (within same machine)

- The Internet (TCP/IP, UDP/IP)

- Things "no one" uses anymore (OSI, Appletalk, IPX, ...)

**Socket Creation**

File systems provide a collection of permanent objects in a structured name space:

- Processes open, read/write/close them

- Files exist independently of processes

- Easy to name what file to open()

Pipes: one-way communication between processes on same (physical) machine

- Single queue

- Created transiently by a call to pipe()

- Passed from parent to children (descriptors inherited from parent process)

Sockets: two-way communication between processes on same or different machine

- Two queues (one in each direction)

- Processes can be on separate machines: no common ancestor

**Namespaces for Communication over IP**

The IP address is not enough. If you have a browser with a bunch of tabs in it, each one of those tabs has the same IP address because there's only one machine. And so you need a way to uniquely name a connection, and that's where ports come into play.

- Hostname
  
  - `www.eecs.berkeley.edu`

- IP address
  
  - `128.32.244.172` (IPv4, 32-bit Integer)
  
  - `2607:f140:0:81::f` (IPv6, 128-bit Integer)

- Port Number
  
  - $0$ ~ $1023$ are "well known" or "system" ports
    
    - Superuser privileges to bind to one
  
  - $1024$ ~ $49151$ are "registered" ports (registry)
    
    - Assigned by IANA for specific services
  
  - $49152$ ~ $65535$ ($2^{15}+2^{14}$ to $2^{16}-1$) are "dynamic" or "private"
    
    - Automatically allocated as "ephemeral ports"

<u>*A port is a 16 bit integer that helps define a unique connection.*</u>

Ports are part of the TCP/IP and UDP/IP spec. There's 16 bits, so there's only really 65536 of them. And the first 1024 are called well known, and the well known ports are ones that are much harder for you to bind anything to, and in fact, you're going to need to be super user to use them. There are some ports between 1024 and 49151 which are typically registered ports. Like for instance, 25565 happens to be the port for Minecraft server. And then there's a bunch of dynamic ports or private ones.

**Connection Setup over TCP/IP**

Special kind of socket: server socket

- Has file descriptor

- Can't read or write

The server needs to set up the process of waiting for a client to connect, and that's called a server socket. So the server basically produces a server socket, and that server socket listens on typically well known ports that have been registered with a standardization agency. And you can register them, but it's very hard to get the ports in that lower 1024 registered.

Typically, people have ports that are just well known in the higher portions. But now once the server socket is set up, now the client will be able to communicate, which is because this cocket, the thing the server does after creating it is listen, which says go to sleep waiting for an incoming connection. So this client creates its end of the socket, sets a request to the other end by using the IP address and the standard port, and the server executes an accept.

Ping does not set up a connection. Ping is the ICMP protocol, which is just a datgram protocol.

Two operations:

1. listen(): Start allowing clients to connect

2. accept(): Create a new socket for a particular client

5-Tuple identifies each connection:

1. Source IP Address

2. Destination IP Address

3. Source Port Number

4. Destination Port Number

5. Protocol (always TCP here)

Often, Client Port "randomly" assigned

- Done by OS during client socket setup

Server Port often "well known"

- 80 (web), 443(secure web), 25(sendmail), etc

- Well-known ports from 0 ~ 1023

80 is a common one that's web browsing without any security. 443 is the HTTPS protocol, 25 is send mail, etc.

All the server sockets are not operating out of the same port. There's one server socket operating on a port 80 and it spawns all the new sockets that are communicating with port 80.

The client side of the connection is typically in that upper range above 49000 of randomly or dynamically assigned port numbers. So when a client first does this connection, they assign themselves a random port. So now they have their IP address, a random new port for that connection.

The server side has its own IP address. Each server socket has a particular port that it's bound to. If this were a web server, it would be bound to port 80.

**Client Protocol**

```c
char *host_name, *port_name;

// Create a socket
struct addrinfo *server = lookup_host(host_name, port_name);
int sock_fd = socket(server->ai_family, server->ai_socktype,
                    server->ai_protocol);

// Connect to specified host and port
connect(sock_fd, server->ai_addr, server->ai_addrlen);

// Carry out Client-Server protocol
run_client(sock_fd);


// Clean up on termination
close(sock_fd);
```

**Server Protocol (v1)**

```c
// Create socket to listen for client connections
char *port_name;
struct addrinfo *server = setup_address(port_name);
int server_socket = socket(server->ai_family,
    server->ai_socktype, server->ai_protocol);


// Bind socket to specific port
bind(server_socket, server->ai_addr, server->ai_addrlen);
// Start listening for new client connections
listen(server_socket, MAX_QUEUE);


while(1){
    // Accept a new client connection, obtaining a new socket
    int conn_socket = accept(server_socket, NULL, NULL);
    serve_client(conn_socket);
    close(conn_socket);
}
close(server_socket);
```

**Concurrent Server**

A concurrent server can handle and service a new connection before the previous client disconnects

**Server Protocol (v2)**

```c
// Socket setup code elided...
while(1){
    // Accept a new client connection, obtaining a new socket
    int conn_socket = accept(server_socket, NULL, NULL);
    pid_t pid = fork();
    if (pid == 0) {
        close(server_socket);
        serve_client(conn_socket);
        close(conn_socket);
        exit(0);
    } else {
        close(conn_socket);
        wait(NULL);
    }
}
close(server_socket);
```

**Server Protocol (v3)**

```c
// Socket setup code elided...
while(1){
    // Accept a new client connection, obtaining a new socket
    int conn_socket = accept(server_socket, NULL, NULL);
    pid_t pid = fork();
    if (pid == 0) {
        close(server_socket);
        serve_client(conn_socket);
        close(conn_socket);
        exit(0);
    } else {
        close(conn_socket);
        // wait(NULL);
    }
}
close(server_socket);
```

**Server Address: Itself**

```c
struct addrinfo *setup_address(char *port) {
    struct addrinfo *server;
    struct addrinfo hints;
    memset(&hints, 0, sizeof(hints));
    hints.ai_family = AF_UNSPECl
    hints.ai_socktype = SOCK_STREAM;
    hints.ai_flags = AI_PASSIVE;
    getaddrinfo(NULL, port, &hints, &server);
    return server;
}
```

- Accepts any connections on the specified port

**Client: Getting the Server Address**

```c
struct addrinfo *lookup_host(char *host_name, char *port) {
    struct addrinfo *server;
    struct addrinfo hints;
    memset(&hints, 0, sizeof(hints));
    hints.ai_family = AF_UNSPEC;
    hints.ai_socktype = SOCK_STREAM;

    int rv = getaddrinfo(host_name, port_name,
                        &hints, &server);
    if(rv != 0){
        printf("getaddrinfo failed: %s\n", gai_strerror(rv));
    }
    return server;
}
```

**Thread Pools**

Problem with previous version: Unbounded Threads

- When web-site becomes too popular - throughput sinks

Instead, allocate a bounded "pool" of worker threads, representing the maximum level of multiprogramming

```
master(){
    allocThreads(worker,queue);
    while(TRUE){
        con=AcceptCon();
        Enqueue(queue,con);
        wakeUp(queue);
    }
}
```

```
worker(queue){
    while(TRUE){
        con=Dequeue(queue);
        if(con==null)
            sleepOn(queue);
        else
            ServiceWebPage(con);
    }
}
```

---

**Multiplexing Processes: The Process Control Block**

Kernel represents each process as a process control block (PCB)

- Status (running, ready, blocked, ...)

- Register state (when not ready)

- Process ID (PID), User, Executable, Priority, ...

- Execution time, ...

- Memory space, translation, ...

Kernel Scheduler maintains a data structure containing the PCBs

- Give out CPU to different processes

- This is a Policy Decision

Give out non-CPU resources

- Memory/IO

- Another policy decision

```
| process state      |
| process number     |
| program counter    |
| registers          |
| memory limits      |
| list of open files |
| ...                |

Process Control Block
```

For x86, there's actually four privilege levels, but you typically only use zero and three. In some early versions of things where level 0 is actually the Hypervisor and level 1 is the kernel level and so on.

**Lifecycle of a Process or Thread**

As a process executes, it changes state:

- new: The process/thread is being created

- ready: The process is waiting to run

- running: Instructions are being executed

- waiting: Process waiting for some event to occur

- terminated: The process has finished execution

**Scheduling: All About Queues**

PCBs move from queue to queue

Scheduling: which order to remove from queue

**Ready Queue And Various I/O Device Queues**

Process not running => PCB is in some scheduler queue

- Separate queue for each device / signal / condition

- Each queue can have a different scheduler policy

**Scheduler**

```c
if(readyProcesses(PCBs)){
    nextPCB = selectProcess(PCBs);
    run(nextPCB);
} else {
    run_idle_process();
}
```

Scheduling: Mechanism for deciding which processes/threads receive the CPU

**The Core of Concurrency: the Dispatch Loop**

Conceptually, the scheduling loop of the operating system looks as follows:

```c
Loop {
    RunThread();
    ChooseNextThread();
    SaveStateOfCPU(curTCB);
    LoadStateOfCPU(newTCB);
}
```

This is an infinite loop

- One could argue that this is all that the OS does

**Running a thread**

Consider first portion: RunThread()

- How do I run a thread?
  
  - Load its state (registers, PC, stack pointer) into CPU
  
  - Load environment (virtual memory space, etc)
  
  - Jump to the PC

- How does the dispatcher get control back?
  
  - Internal events: thread returns control voluntarily
  
  - External events: thread gets preempted

**Internal Events**

Blocking on I/O

- The act of requesting I/O implicitly yields the CPU

- Waiting on a "signal" from other thread
  
  - Thread asks to wait and thus yields the CPU

- Thread executes a yield()
  
  - Thread volunteers to give up CPU

```c
computePI() {
    while(TRUE) {
        ComputeNextDigit();
        yield();
    }
}
```

**Stack for Yielding Thread**

| ComputePI          |
|:------------------:|
| **yield**          |
| **kernel_yield**   |
| **run_new_thread** |
| **switch**         |

How do we run a new thread?

```c
run_new_thread(){
    newThread = PickNewThread();
    switch(curThread, )
}
```

How does dispatcher switch to a new thread?

- Save anything next thread may trash: PC, regs, stack pointer

- Maintain isolation for each thread

**Saving/Restoring state (often called "Context Switch")**

```assembly
Switch(tCur, tNew){
    /* Unload old thread*/
    TCB[tCur].regs.r7 = CPU.r7;
        ...
    TCB[tCur].regs.r0 = CPU.r0;
    TCB[tCur].regs.sp = CPU.sp;
    TCB[tCur].regs.retpc = CPU.retpc; /* return addr */

    /* Load and execute new thread */
    CPU.r7 = TCB[tNew].regs.r7;
        ...
    CPU.r0 = TCB[tNew].regs.r0;
    CPU.sp = TCB[tNew].regs.sp;
    CPU.retpc = TCB[tNew].regs.retpc;
    return; /* Return to CPU.retpc */
}
```

**Switch Details**

TCB+Stacks (user/kernel) contains complete restartable state of Thread!

- Can put it on any queue for later revival!

What if you make a mistake in implementing switch?

- Suppose you forget to save/restore register 32

- Get intermittent failures depending on when context switch occurred and whether new thread uses register 32

- Get intermittent failures depending on when context switch occurred and whether new thread uses register 32

- System will give wrong result without warning

Can you devise an exhaustive test to test switch code?

- No! Too many combinations and inter-leavings

Cautionary tale:

- For speed, Topaz kernel saved one instruction in switch()

- Carefully documented! Only works as long as kernel size < 1MB

- What happened?
  
  - Time passed, People forgot.
  
  - Later, they added features to kernel (no one removes features!)
  
  - Very weird behavior started happening

- Moral of story: Design for simplicity

There's a kernel from digital equipment corporations, one of their research labs called topaz. And this was back in the days where memory was very scarce. And so some very clever programmer decided to save an instruction and switch that worked fine as long as the kernel wasn't bigger than a megabyte.

Be sure that you design for simplicity. And if you're going to make some micro optimization, you better make sure it's really worth it.

**We are still switching contexts**

But much cheaper than switching processes

- No need to change address space

Some numbers from Linux:

- Frequency of context switch: 10 ~ 100ms

- Switching between processes: 3 ~ 4 $\mu$sec.

- Switching between threads: 100 ns

Even cheaper: switch threads (using "yield") in user-space!

- Simple One-to-One Threading Model

- Many-to-One

- Many-to-Many

While the user thread models very fast, it doesn't interact with sleeping in the kernel well. And so that's why there's also a many to many model where you have a small number of kernel threads and many more user threads.

**Processes vs. Threads**

*One CPU, each process may have multiple threads and there might be multiple processes:*

- Switch overhead:
  
  - Same process: low
  
  - Different proc: high

- Protection
  
  - Same proc: low
  
  - Different proc: high

- Sharing overhead
  
  - Same proc: low
  
  - Different proc: high

- Parallelism: no

*Multiple cores, introduce parallelism:*

- Switch overhead:
  
  - Same process: low
  
  - Different proc: high

- Protection:
  
  - Same proc: low
  
  - Different proc: high

- Sharing overhead
  
  - Same proc: low
  
  - Different proc,
    
    simultaneous core: medium
  
  - Different proc,
    
    offloaded core: high

- Parallelism: yes

**Simultaneous MultiThreading/Hyperthreading**

Hardware scheduling technique

- Superscalar processors can execute multiple instructions that are independent.

- Hyperthreading duplicates register state to make a second "thread", allowing more instructions to run.

Can schedule each thread as if were separate CPU

- But, sub-linear speedup!

Original technique called "Simultaneous Multithreading"

- http://www.cs.washington.edu/research/smt/index.html

- SPARC, Pentium 4/Xeon ("Hyperthreading"), Power 5

GPU don't really quite have hyper threading in the way you're thinking. GPU are usually designed as a single task takes over the whole GPU. Hyper threadings shouldn't affect locking, because if you've got a good code, that will work under all circumstances of concurrency and parallelism, it shouldn't matter.

Hyper threading is parallel because there's two actual threads and they are running simultaneously.

What happens when a thread requests a block of data from the file system?

- User code invokes a system call

- Read operation is initiated

- Run new thread/switch

Thread communication similar

- Wait for Signal/Join

- Networking

**External Events**

What happens if thread never does any I/O, never waits, and never yields control?

- Could the ComputePI program grab all resources and never release the processor?
  
  - What if it didn't print to console?

- Must find way that dispatcher can regain control!

Answer: utilize external events

- Interrupts: signals from hardware or software that stop the running code and jump to kernel

- Timer: like an alarm clock that goes off every some milliseconds

If we make sure the external events occur frequently enough, then we get fair sharing of the CPU as well.

**Interrupt Controller**

A typical CPU has a bunch of devices that are all connected via interrupt lines to an interrupt controller. And that interrupt controller goes through an interrupt mask, which lets us to disable interrupts, and then that goes through an encoder and tells the CPU to stop what it's doing to handle and interrupt.

- Interrupts invoked with interrupt lines from devices

- Interrupt controller chooses interrupt request to honor
  
  - Interrupt identity specified with ID line
  
  - Mask enables/disables interrupts
  
  - Priority encoder picks highest enabled interrupt
  
  - Software Interrupt Set/Cleared by Software

- CPU can disable all interrupts with internal flag

- Non-Maskable interrupt line (NMI) can't be disabled

The kernel stack is in kernel memory, that's correct and it's not, and when you're at user level, you can't access that kernel stack. Otherwise that would defeat the whole port.

An interrupt is a hardware-invoked context switch

- No separate step to choose what to run next

- Always run the interrupt handler immediately

**Use of Timer Interrupt to Return Control**

Solution to our dispatcher problem

- Use the timer interrupt to force scheduling decisions

Timer Interrupt routine:

```
TimerInterrupt(){
    DoPeriodicHouseKeeping();
    run_new_thread();
}
```

**Initialize TCB and Stack**

Initialize Register fields of TCB

- Stack pointer made to point at stack

- PC return address => OS (asm) routine ThreadRoot()

- Two arg registers (a0 and a1) initialized to fcnPtr and fcnArgPtr, respectively

Initialize stack data?

- No. Important part of stack frame is in registers (ra)

- Think of stack frame as just before body of ThreadRoot() really gets started

How do we make a new thread?

- Setup TCB/kernel thread to point at new user stack and ThreadRoot code

- Put pointers to start function and args in registers

- This depends heavily on the calling convention (i.e. RISC-V vs x86)

```c
SetupNewThread(tNew) {
    ...
    TCB[tNew].regs.sp = newStackPtr;
    TCB[tNew].regs.retpc = &ThreadRoot;
    TCB[tNew].regs.r0 = fcnPtr;
    TCB[tNew].regs.r1 = fcnArgPtr
}
```

ThreadRoot() is the root for the thread routine:

```c
ThreadRoot(fcnPTR,fcnArgPtr) {
    DoStartupHousekeeping();
    UserModeSwitch(); /* enter user mode */
    Call fcnPtr(fcnArgPtr);
    ThreadFinish();
}
```

Startup Housekeeping

- Includes things like recording start time of thread

- Other statistics

Stack will grow and shrink with execution of thread

**Correctness with Concurrent Threads**

- Non-determinism:
  
  - Scheduler can run threads in any order
  
  - Scheduler can switch threads at any time
  
  - This can make testing very difficult

- Independent Threads
  
  - No state shared with other threads
  
  - Deterministic, reproducible conditions

- Cooperating Threads
  
  - Shared state between multiple threads

Goal: Correctness by Design

**ATM Bank Server**

ATM server problem:

- Service a set of requests

- Do so without corrupting database

- Don't hand out too much money

Suppose we wanted to implement a server process to handle requests from an ATM network:

```c
BankServer() {
    while(TRUE){
        ReceiveRequest(&op, &acctId, &amount);
        ProcessRequest(&op, acctId, amount);
    }
}
ProcessRequest(op, acctId, amount) {
    if(op == deposit) Deposit(acctId, amount);
    else if ...
}
Deposit(acctId, amount) {
    acct = GetAccount(acctId); /* may use disk I/O */
    acct->balance += amount;
    StoreAccount(acct); /* Involves disk I/O */
}
```

How could we speed this up?

- More than one request being processed at once

- Event driven (overlap computation and I/O)

- Multiple threads (Multi-proc, or overlap comp and I/O)

***Event Driven Version of ATM server***

- Suppose we only had one CPU
  
  - Still like to overlap I/O with computation
  
  - Without threads, we would have to rewrite in event-driven style

- Example
  
  ```c
  BankServer() {
      while(TRUE) {
          event = WaitForNextEvent();
          if (event == ATMRequest)
              StartOnRequest();
          else if (event == AcctAvail)
              ContinueRequest();
          else if (event == AcctStored)
              FinishRequest();
      }
  }
  ```
  
  - What if we missed a blocking I/O step?
  
  - What if we have to split code into hundreds of pieces which could be blocking?
  
  - This technique is used for graphical programming

***Threads***

- Threads yield overlapped I/O and computation without "deconstructing" code into non-blocking fragments
  
  - One thread per request

- Requests proceeds to completion, blocking as required:
  
  ```c
  Deposit(acctId, amount) {
      acct = GetAccount(actId); /* May use disk I/O */
      acct->balance += amount;
      StoreAccount(acct);    /* Involves disk I/O */
  }
  ```

- Unfortunately, shared state can get corrupted:
  
  | Thread 1                | Thread 2               |
  |:-----------------------:|:----------------------:|
  | load r1, acct->balance  |                        |
  |                         | load r1, acct->balance |
  |                         | add r1, amount2        |
  | add r1, amount1         |                        |
  | store r1, acct->balance |                        |

***Atomic Operations***

- To understand a concurrent program, we need to know what the underlying indivisible operations are!

- Atomic Operation: an operation that always runs to completion or not all
  
  - It is indivisible: it cannot be stopped in the middle and state cannot be modified by someone else in the middle
  
  - Fundamental building block - if no atomic operations, then have no way for threads to work together

On most machines, memory references and assignments (i.e. loads and stores) of words are atomic

- Consequently - wierd example that produces "3" on previous slide can't happen

Many instructions are not atomic

- Double-precision floating point store often not atomic

- VAX and IBM 360 had an instruction to copy a whole array

***Fix banking problem with Locks***

Identify critical sections (atomic instruction sequences) and add locking:

```c
Deposit(acctId, amount) {
    acquire(&mylock) // Wait if someone else in critical section!
    acct = GetAccount(actId); // Critical Section
    acct->balance += amount;
    StoreAccount(acct);
    release(&mylock) // Release someone into critical section
}
```

Threads serialized by lock through critical section. Only one thread at a time.

Must use SAME lock (mylock) with all of the methods (Withdraw, etc...)

- Shared with all threads!

**Concurrency is Hard**

- Even for practicing engineers trying to write mission-critical, bulletproof code!
  
  - Threaded programs must work for all interleavings of thread instruction sequences
  
  - Cooperating threads inherently non=deterministic and non-reproducible
  
  - Really hard to debug unless carefully designed!

- Therac-25: Radiation Therapy Machine with Unintended Overdoses
  
  - Concurrency errors caused the death of a number of patients by misconfiguring the radiation production
  
  - Improper synchronization between input from operators and positioning software

- Mars Pathfinder Priority Inversion

- Toyota Uncontrolled Acceleration
  
  - 256.6K Lines of C Code, ~9-11K global variables
  
  - Inconsistent mutual exclusion on reads/writes

---

**Producer-Consumer with a Bounded Buffer**

Problem Definition

- Producer(s) put things into a shared buffer

- Consumer(s) take them out

- Need synchronization to coordinate producer/consumer

Don't want producer and consumer to have to work in lockstep, so put a fixed-size buffer between them

- Need to synchronize access to this buffer

- Producer needs to wait if buffer is full

- Consumer needs to wait if buffer is empty

Example: GCC compiler, Coke machine, Web Servers, Routers, ...

**Higher-level Primitives than Locks**

What is right abstraction for synchronizing threads that share memory?

- Want as high a level primitive as possible

Good primitives and practices important!

- Since execution is not entirely sequential, really hard to find bugs, since they happen rarely

- UNIX is pretty stable now, but up until about mid-80s
  
  (10 years after started), systems running UNIX would crash every week or so - concurrency bugs

Synchronization is a way of coordinating multiple concurrent activities that are using shared state

**Semaphores**

Semaphores are like integers, except:

- No negative values

- Only operations allowed are P and V - can't read or write value, except initially

- Operations must be atomic
  
  - Two P's together can't decrement value below zero
  
  - Thread going to sleep in P won't miss wakeup from V - even if both happen at same time

- POSIX adds ability to read value, but technically not part of proper interface!

**C Language Support for Synchronization**

C language: Pretty straightforward synchronization

- Just make sure you know all the code paths out of a critical section
  
  ```c
  int Rtn() {
      acquire(&lock);
      ...
      if(exception){
          release(&lock);
          return errReturnCode;
      }
      ...
      release(&lock);
      return OK;
  }
  ```
  
  Watch out for `setjmp/longjmp`!
  
  - Can cause a non-local jump out of procedure

**C++ Language Support for Synchronization**

Languages with exceptions like C++

- Languages that support exceptions are problematic (easy to make a non-local exit without releasing lock)

- Consider:
  
  ```cpp
  void Rtn() {
      lock.acquire();
      ...
      DoFoo();
      ...
      lock.release();
      }
      void DoFoo() {
          ...
          if (exception) throw errException;
      }
  }
  ```
  
  Notice that an exception in DoFoo() will exit without releasing the lock!

**C++ Lock Guards**

```cpp
#include <mutex>
int global_i = 0;
std::mutex global_mutex;

void safe_increment() {
    std::lock_guard<std::mutex> lock(global_mutex);
    ...
    global_i++;
    // Mutex released when 'lock' goes out of scope
}
```

**Python with keyword**

More versatile than we show here (can be used to close files, database connections, etc.)

```python
lock = threading.Lock()
...
with lock: # Automatically calls acquire()
    some_var += 1
    ...
    # release() called however we leave block
```

**Java synchronized Keyword**

Every Java object has an associated lock:

- Lock is acquired on entry and released on exit from a synchronized method

- Lock is properly released if exception occurs inside a synchronized method

- Mutex execution of synchronized methods (beware deadlock)

```java
class Account {
    private int balance;

    // object constructor
    public Account (int intialBalance) {
        balance = initialBalance;
    }

    public synchronized int getBalance() {
        return balance;
    }

    public synchronized void deposit(int amount) {
        balance += amount;
    }
}
```

**Java Support for Monitors**

Along with a lock, every object has a single condition variable associated with it

To wait inside a synchronized method:

```java
void wait();
```

```java
void wait(long timeout);
```

To signal while in a synchronized method:

```java
void notify();
```

```java
void notifyAll();
```

**In Pintos, Processes are Single-Threaded**

Pintos processes have only one thread

TCB: Single page (4KB)

- Stack growing from the top (high addresses)

- struct thread at the bottom (low addresses)

struct thread defines the TCB structure and PCB structure in Pintos

**(Aside): Linux "Task"**

Linux "Kernel Thread": 2 pages (8 KiB)

- Stack and thread information on opposite sides

- Containing stack and thread information + process descriptor

One task_struct per thread

**Multithreaded Processes (not in Pintos)**

Traditional implementation strategy:

- One PCB (process struct) per process

- Each PCB contains (or stores pointers to) each thread's TCB

Linux's strategy:

- One task_struct per thread

- Threads belonging to the same process happen to share some resources
  
  - Like address space, file descriptor table, etc.

**Timer may trigger thread switch**

- thread_tick
  
  - Updates thread counters
  
  - If quanta exhausted, sets yield flag

- thread_yield
  
  - On path to rtn from interrupt
  
  - Sets current thread back to READY
  
  - Pushes it back on ready_list
  
  - Calls shedule to select next thread to run upon iret

- Schedule
  
  - Selects next thread to run
  
  - Calls switch_threads to change regs to point to stack for thread to resume
  
  - Sets its status to RUNNING
  
  - If user thread, activates the process
  
  - returns back to interrupt handler

**Famous Quote WRT Scheduling: Dennis Richie**

```
Dennis Richie,

Unix V6, slp.c:

/*
* If the new process paused because it was
* swapped out, set the stack level to the last call
* to savu(ssav). This means that the return
* which is executed immediately after the call to aretu
* actually returns from the last routine which did
* the savu.
* 
* You are not expected to understand this
*/
```

---

**Device Drivers**

Device Driver: Device-specific code in the kernel that interacts directly with the device hardware

- Supports a standard, internal interface

- Same kernel I/O system can interact easily with different device drivers

- Special device-specific configuration supported with the `ioctl()` system call

Device Drivers typically divided into two pieces:

- Top half: accessed in call path from system calls
  
  - implements a set of standard, cross-device calls like open(), close(), read(), write(), ioctl(), strategy()
  
  - This is the kernel's interface to the device driver
  
  - Top half will start I/O to device, may put thread to sleep until finished

- Bottom half: run as interrupt routine
  
  - Gets input or transfers next block of output
  - May wake sleeping threads if I/O now complete

**Life Cycle of An I/O Request**

| User Program                  |
|:-----------------------------:|
| **Kernel I/O Subsystem**      |
| **Device Driver Top Half**    |
| **Device Driver Bottom Half** |
| **Device Hardware**           |

**Scheduling Assumptions**

In the seventies, scheduling was kind of a big area of research. Computer were new enough that people hadn't really figured things out. And the usage models were pretty basic because people had mainframes in big rooms. And those were multi-million dollar machines, and you had a bunch of people using them. So you had to somehow make sure that those super million dollar resources were properly shared among different users because they were just expensive. And you couldn't let a user take too much time, but you also couldn't let a user who's maybe spent money for computer time be upset because they're not getting their fair share.

- CPU scheduling big area of research in early 70's

- Many implicit assumptions for CPU scheduling:
  
  - One program per user
  
  - One thread per program
  
  - Programs are independent

- Clearly, these are unrealistic but they simplify the problem so it can be solved
  
  - For instance: is "fair" about fairness among users or programs?
    
    - If I run one compilation job and you run five, you get five times as much CPU on many operating systems

- The high-level goal: Dole out CPU time to optimize some desired parameters of system

More and more people have CPU's of their own, so they have lots of cell phones and other things, you're going to want to be cognizant of responsiveness.

**Scheduling Policy Goals/Criteria**

Minimize Response Time

- Minimize elapsed time to do an operation (or job)

- Response time is what the user sees:
  
  - Time to echo a keystroke in editor
  
  - Time to compile a program
  
  - Real-time Tasks: Must meet deadlines imposed by World

Maximize Throughput

- Maximize operations (or jobs) per second

- Throughput related to response time, but not identical:
  
  - Minimizing response time will lead to more context switching than if you only maximized throughput

- Two parts to maximizing throughput
  
  - Minimize overhead (for example, context-switching)
  
  - Efficient use of resources (CPU, disk, memory, etc)

Fairness

- Share CPU among users in some equitable way

- Fairness is not minimizing average response time:
  
  - Better average response time by making system less fair

**First-Come, First-Served (FCFS) Scheduling**

First-Come, First-Served (FCFS)

- Also "First In, First Out" (FIFO) or "Run until done"
  
  - In early systems, FCFS meant one program
    
    sheduled until done (including I/O)
  
  - Now, means keep CPU until thread blocks

**Convoy effect**

With FCFS non-preemptive scheduling, convoys of small tasks tend to build up when a large one is running.

**Round Robin (RR) Scheduling**

- FCFS Scheme: Potentially bad for short jobs!
  
  - Depends on submit order
  
  - If you are first in line at supermarket with milk, you don't care who is behind you, on the other hand...

- Round Robin Scheme: Preemption!
  
  - Each process gets a small unit of CPU time
    
    (time quantum), usually 10~100 milliseconds
  
  - After quantum expires, the process is preempted and added to the end of the ready queue.

- n processes in ready queue and time quantum is q =>
  
  - Each process gets $\frac{1}{n}$ of the CPU time
  
  - In chunks of at most $q$ time units
  
  - No process waits more than $(n-1)q$ time units

- Performance
  
  - $q$ large => FCFS
  
  - $q$ small => Interleaved (really small => hyperthreading?)
  
  - $q$ must be large with respect to context switch, otherwise overhead is too high (all overhead)

**Round-Robin Discussion**

How do you choose time slice?

- What if too big?
  
  - Response time suffers

- What if infinite($\infty$)?
  
  - Get back FIFO

- What if time slice too small?
  
  - Throughput suffers!

Actual choices of timeslice:

- Initially, UNIX timeslice one second:
  
  - Worked ok when UNIX was used by one or two people
  
  - What if three compilations going on? 3 seconds to echo each keystroke!

- Need to balance short-job performance and long-job throughput:
  
  - Typical time slice today is between 10ms ~ 100ms
  
  - Typical context-switching overhead is 0.1ms ~ 1ms
  
  - Roughly 1% overhead due to context-switching

Comparisons between FCFS and Round Robin

Assuming zero-cost context-switching time, is RR always better than FCFS?

Simple example:

10 jobs, each take 100s of CPU time RR scheduler quantum of 1s

All jobs start at the same time

- Completion Times: 
  
  | Job # | FIFO | RR   |
  |:-----:|:----:|:----:|
  | 1     | 100  | 991  |
  | 2     | 200  | 992  |
  | ...   | ...  | ...  |
  | 9     | 900  | 999  |
  | 10    | 1000 | 1000 |
  
  Both RR and FCFS finish at the same time
  
  Average response time is much worse under RR!
  
  - Bad when all jobs same length

- Also: Cache state must be shared between all jobs with RR but can be devoted to each job with FIFO
  
  - Total time for RR longer even for zero-cost switch!

**Scheduling Fairness**

What about fairness?

- Strict fixed-priority scheduling between queues is unfair (run highest, then next, etc):
  
  - long running jobs may never get CPU
  
  - Urban legend: In Multics, shut down machine, found 10-year-old job => probably not...

- Must give long-running jobs a fraction of the CPU even when there are shorter jobs to run

- Tradeoff: fairness gained by hurting avg response time!

How to implement fairness?

- Could give each queue some fraction of the CPU
  
  - What if one long-running job and 100 short-running ones?
  
  - Like express lanes in a supermarket - sometimes express lanes get so long, get better service by going into one of the other lines

- Could increase priority of jobs that don't get service
  
  - What is done in some variants of UNIX
  
  - This is ad hoc - what rate should you increase priorities?
  
  - And, as system gets overloaded, no job gets CPU time, so everyone increases in priority => Interactive jobs suffer

**Predicting the Length of the Next CPU Burst**

Adaptive: Changing policy based on past behavior

- CPU scheduling, in virtual memory, in file systems, etc

- Works because programs have predictable behavior
  
  - If program was I/O bound in past, likely in future
  
  - If computer behavior were random, wouldn't help

**Lottery Scheduling**

Yet another alternative: Lottery Scheduling

- Give each job some number of lottery tickets

- On each time slice, randomly pick a winning ticket

- On average, CPU time is proportional to number of tickets given to each job

How to assign tickets?

- To approximate SRTF, short running jobs get more, long running jobs get fewer

- To avoid starvation, every job gets at least one ticket (everyone makes progress)

Advantage over strict priority scheduling: behaves gracefully as load changes

- Adding or deletig a job affects all jobs proportionally, independent of how many tickets each job possesses

**How to Evaluate a Scheduling algorithm**

Deterministic modeling

- takes a predetermined workload and compute the performance of each algorithm for that workload

Queueing models

- Mathematical approach for handling stochastic workloads

Implementation/Simulation:

- Build system which allows actual algorithms to be run against actual data

- Most flexible/general

---

**Linux O(1) Scheduler**

| Kernel/Realtime Tasks | User Tasks |
|:---------------------:| ---------- |

Priority-based scheduler: 140 priorities

- 40 for "user tasks" (set by "nice"), 100 for "Realtime/Kernel"

- Lower priority value => higher priority (for nice values)

- Highest priority value => Lower priority (for realtime values)

- All algorithms O(1)
  
  - Timeslices/priorities/interactivity credits all computed when job finishes time slice
  
  - 140-bit bit mask indicates presence or absence of job at given priority level

Two separate priority queues: "active" and "expired"

- All tasks in the active queue use up their timeslices and get placed on the expired queue, after which queues swapped

Timeslice depends on priority - linearly mapped onto timeslice range

- Like a multi-level queue (one queue per priority) with different timeslice at each level

Lots of ad-hoc heuristics

- Try to boost priority of I/O-bound tasks

- Try to boost priority of starved tasks

Heuristics

- User-task priority adjusted ±5 based on heuristics
  
  - p->sleep_avg = sleep_time - run_time
  
  - Higher sleep_avg => more I/O bound the task, more reward (and vice versa)

- Interactive Credit
  
  - Earned when a task sleeps for a "long" time
  
  - Spend when a task runs for a "long" time
  
  - IC is used to provide hysteresis to avoid changing interactivity for temporary changes in behavior

However, "interactive tasks" get special dispensation

- To try to maintain interactivity

- Placed back into active queue, unless some other task has been starved for too long...

Real-Time Tasks

- Always preempt non-RT tasks

- No dynamic adjustment of priorities

- Scheduling schemes:
  
  - SCHED_FIFO: preempts other tasks, no timeslice limit
  
  - SCHED_RR: preempts normal tasks, RR scheduling amongst tasks of same priority

If you're the core developer of some operating system that's used by a whole bunch of people and they have relied on the behavior of your scheduler and its heuristics, and however, somebody isn't quite happy, so you need to change something. You don't want to change the heuristics too much, because now everybody else is going to be unhappy.

**Does the OS Schedule Processes or Threads?**

Many textbooks use the "old model" - one thread per process

Usually it's really: threads (e.g., in Linux)

One point to notice: switching threads vs. switching processes incurs different costs:

- Switch threads: Save/restore registers

- Switch processes: Change active address space too!
  
  - Expensive
  
  - Disrupts caching

Recall, However: Simultaneous Multithreading (or "Hyperthreading")

- Different threads interleaved on a cycle-by-cycle basis and can be in different processes (have different address spaces)

**Multi-Core Scheduling**

Algorithmically, not a huge difference from single-core scheduling

Implementation-wise, helpful to have per-core scheduling data structures

- Cache coherence

Affinity scheduling: once a thread is scheduled on a CPU, OS tries to reschedule it on the same CPU

- Cache reuse

**Gang Scheduling and Parallel Applications**

When multiple threads work together on a multi-core system, try to schedule them together

- Makes spin-waiting more efficient (inefficient to spin-wait for a thread that's suspended)

Alternative: OS informs a parallel program how many processors its threads are scheduled on (Scheduler Activations)

- Application adapts to number of cores that it has scheduled

- "Space sharing" with other parallel programs can be more efficient, because parallel speedup is often sublinear with the number of cores

**Real-Time Scheduling**

Goal: Predictability of Performance!

- We need to predict with confidence worst case response times for systems!

- In RTS, performance guarantees are:
  
  - Task - and/or class centric and often ensured a priori

- In conventional systems, performance is:
  
  - System/throughput oriented with post-processing (... wait and see ...)

- Real-time is about enforcing predictability, and does not equal fast computing!

Hard real-time: for time-critical safety-oriented systems

- Meet all deadlines (if at all possible)

- Ideally: determine in advance if this is possible

- Earliest Deadline First (EDF), Least Laxity First (LLF),
  
  Rate-Monitonic Scheduling (RMS), Deadline Monotonic Scheduling (DM)

- Soft real-time: for multimedia
  
  - Attempt to meet deadlines with high probability
  
  - Constant Bandwidth Server (CBS)

**Earliest Deadline First (EDF)**

Tasks periodic with period P and computation C in each period: $(P_i,C_i)$ for each task $i$

Preemptive priority-based dynamic scheduling:

- Each task is assigned a (current) priority based on how close the absolute deadline is (i.e. $D_{i}^{t+1}=D_i^{t}+P_i$ for each task)

- The scheduler always schedules the active task with the closest absolute deadline

**Strawman: Last-Come, First-Served (LCFS)**

- Stack (LIFO) as a scheduling data structure
  
  - Late arrivals get fast service
  
  - Early ones wait - extremely unfair
  
  - In the worst case - starvation

- When would this occur?
  
  - When arrival rate (offered load) exceeds service rate (delivered load)
  
  - Queue builds up faster than it drains

- Queue can build in FIFO too, but "serviced in the order received" ...

**Martian Pathfinder Rover**

July 4, 1997 - Pathfinder lands on Mars

- First US Mars landing since Vikings in 1976; first rover

- Novel delivery mechanism: inside air-filled balloons bounced to stop on the surface from orbit!

And then ... a few days into mission ... :

- Multiple system resets occur to realtime OS (VxWorks)

- System would reboot randomly, losing valuable time and progress

| Priority 2     | Data Distribution Task: needs lock |
|:--------------:|:----------------------------------:|
| **Priority 1** | **Lots of random medium stuff**    |
| **Priority 0** | **ASI/MET collector: grab lock**   |

Problem? Priority Inversion!

- Low priority task grabs mutex trying to communicate with high priority task:

- Realtime watchdog detected lack of forward progress and invoked reset to safe state
  
  - High-priority data distribution task was supposed to complete with regular deadline

Solution: Turn priority donation back on and upload fixes!

Original developers turned off priority donation (also called priority inheritance)

- Worried about performance costs of donating priority!

**Choosing the Right Scheduler**

| I Care About:                   | Then Choose:       |
|:-------------------------------:|:------------------:|
| CPU Throughput                  | FCFS               |
| Avg. Response Time              | SRTF Approximation |
| I/O Throughput                  | SRTF Approximation |
| Fairness (CPU Time)             | Linux CFS          |
| Fairness - Wait Time to Get CPU | Round Robin        |
| Meeting Deadlines               | EDF                |
| Favoring Important Tasks        | Priority           |

---

**Deadlock: A Deadly type of Starvation**

Starvation: thread waits indefinitely

- Example, low-priority thread waiting for resources constantly in use by high-priority threads

Deadlock: circular waiting for resources

- Thread A owns Res 1 and is waiting for Res 2

- Thread B owns Res 2 and is waiting for Res 1

Deadlock => Starvation but not vice versa

- Starvation can end (but doesn't have to)

- Deadlock can't end without external intervention

**Wormhole-Routed Network**

Circular dependency (Deadlock!)

- Each train wants to turn right, but is blocked by other trains

Similar problem to multiprocessor networks

- Wormhole-Routed Network: Messages trail through network like a "worm"

Fix? Imagine grid extends in all four directions

- Force ordering of channels (tracks)
  
  - Protocol: Always go east-west first, then north-south

- Called "dimension ordering" (X then Y)

**Other Types of Deadlock**

Threads often block waiting for resources

- Locks

- Terminals

- Printers

- CD drives

- Memory

Threads often block waiting for other threads

- Pipes

- Sockets

You can deadlock on any of these!

**Four requirements for occurrence of Deadlock**

***Mutual exclusion***

- Only one thread at a time can use a resource

***Hold and wait***

- Thread holding at least one resource is waiting to acquire additional resources held by other threads

***No preemption***

- Resources are released only voluntarily by the thread holding the resource, after thread is finished with it

***Circular wait***

- There exists a set {$T_1, \dots, T_n$} of waiting threads
  
  - $T_1$ is waiting for a resource that is held by $T_2$
  
  - $T_2$ is waiting for a resource that is held by $T_3$
  
  - $\dots$
  
  - $T_n$ is waiting for a resource that is held by $T_1$

**Detecting Deadlock: Resource-Allocation Graph**

System Model

- A set of Threads $T_1, T_2, \dots , T_n$

- Resource types $R_1, R_2, \dots ,R_m$
  
     *CPU cycles, memory space, I/O devices*

- Each resource type $R_i$ has $W_i$ instances

- Each thread utilizes a resource as follows:
  
     *Request() / Use() / Release()*

Resource-Allocation Graph:

- V is partitioned into two types:
  
  - T = {$T_1, T_2, \dots, T_n$}, the set threads in the system.
  
  - R = {$R_1, R_2, \dots, R_m$}, the set of resource types in system

- request edge - directed edge $T_1$ → $R_j$

- assignment edge - directed edge $R_j$ → $T_1$

**How should a system deal with deadlock?**

Four different approaches:

1. Deadlock prevention: write your code in a way that it isn't prone to deadlock

2. Deadlock recovery: let deadlock happen, and then figure out how to recover from it

3. Deadlock avoidance: dynamically delay resource requests so deadlock doesn't happen

4. Deadlock denial: ignore the possibility of deadlock

Modern operating systems:

- Make sure the system isn't involved in any deadlock 

- Ignore deadlock in applications
  
  - "Ostrich Algorithm"

**Techniques for Preventing Deadlock**

- Infinite resources
  
  - Include enough resources so that no one ever runs out of resources.
    
    Doesn't have to be infinite, just large
  
  - Give illusion of infinite resources (e.g. virtual memory)

- No Sharing of resources (totally independent threads)
  
  - Not very realistic

- Don't allow waiting

- Make all threads request everything they'll need at the beginning
  
  - Problem: Predicting future is hard, tend to over-estimate resources

- Force all threads to request resources in a particular order preventing any cyclic use of resources
  
  - Thus, preventing deadlock

**Banker's Algorithm for Avoiding Deadlock**

Toward right idea:

- State maximum (max) resource needs in advance

- Allow particular thread to proceed if:
  
  (available resources - #requested) $\geq$ max
  
  remaining that might be needed by any thread

Banker's algorithm (less conservative):

- Allocate resources dynamically
  
  - Evaluate each request and grant if some ordering of threads is still deadlock free afterward
  
  - Technique: pretend each request is granted, then run deadlock detection algorithm, substituting:
    
    ([$\text{Max}_{node}$]-[$\text{Alloc}_{node}$])<=[Avail]) for ([$\text{Request}_{node}$])<=[Avail])
    
    Grant request if result is deadlock free (conservative!)

- Keeps system in a "SAFE" state: there exists a sequence {$T_1, T_2, \dots, T_n$} with $T_1$ requesting all remaining resources, finishing, then $T_2$ requesting all remaining resources, etc...

---

**Virtualizing Resources**

- Physical Reality:
  
  Different Processes/Threads share the same hardware
  
  - Need to multiplex CPU (Just finished: scheduling)
  
  - Need to multiplex use of Memory (starting today)
  
  - Need to multiplex disk and devices (later in term)

- Why worry about memory sharing?
  
  - The complete working state of a process and/or kernel is defined by its data in memory (and registers)
  
  - Consequently, cannot just let different threads of control use the same memory
    
    - Physics: two different pieces of data cannot occupy the same locations in memory
  
  - Probably don't want different threads to even have access to each other's memory if in different processes (protection)

**Address/Address Space**

What is $2^{10}$ bytes (where a byte is appreviated as "B")?

- $2^{10}B=1024B=1\text{KB}$    (for memory, 1K=1024, not 1000)

How many bits to address each byte of 4KB page?

- $4\text{KB}=4\times1\text{KB}=4\times2^{10}=2^{12}$ => 12 bits

Use $2^k$

**Address Space, Process Virtual Address Space**

Definition: Set of accessible addresses and the state associated with them

- $2^{32}$ = ~4 billion ***bytes*** on a 32-bit machine

32-bits = 4 bytes, so $\frac{2^{32}}{4}$ = $2^{30}$ =~1 billion

What happens when processor reads or writes to an address?

- Perhaps acts like regular memory

- Perhaps causes I/O operation
  
  (Memory-mapped I/O)

- Causes program to abort (segfault)?

- Communicate with another program

- ...

**Important Aspects of Memory Multiplexing**

Protection:

- Prevent access to private memory of other processes
  
  - Different pages of memory can be given special behavior (Read Only, Invisible to user programs, etc).
  
  - Kernel data protected from User programs
  
  - Programs protected from themselves

Translation:

- Ability to translate accesses from one address space (virtual) to a different one (physical)

- When translation exists, processor uses virtual addresses, physical memory uses physical addresses

- Side effects:
  
  - Can be used to avoid overlap
  
  - Can be used to give uniform view of memory to programs

Controlled overlap:

- Separate state of threads should not collide in physical memory. Obviously, unexpected overlap causes chaos!

- Conversely, would like the ability to overlap when desired (for communication)

**Alternative View: Interposing on Process Behavior**

OS interposes on process' I/O operations

- How? All I/O happens via syscalls.

Os interposes on process' CPU usage

- How? Interrupt lets OS preempt current thread

How can the OS interpose on process' memory accesses?

- Too slow for the OS to interpose every memory access

- Translation: hardware support to accelerate the common case

- Page fault: uncommon cases trap to the OS to handle

**From Program to Process**

Preparation of a program for execution involves components at:

- Compile time (i.e., "gcc")

- Link/Load time (UNIX "Id" does link)

- Execution time (e.g., dynamic libs)

Addresses can be bound to final values anywhere in this path

- Depends on hardware support

- Also depends on operating system

Dynamic Libraries:

- Linking postponed until execution

- Small piece of code (i.e. the stub), locates appropriate memory-resident library routine

- Stub replaces itself with the address of the routine, and executes routine

**Primitive Multiprogramming**

Multiprogramming without Translation or Protection

- Must somehow prevent address overlap between threads

Use Loader/Linker: Adjust addresses while program loaded into memory (loads, stores, jumps)

- Everything adjusted to memory location of program

- Translation done by a linker-loader (relocation)

- Common in early days (... till Windows 3.x, 95?)

With this solution, no protection: bugs in any program can cause other programs to crash or even the OS

**Multiprogramming with Protection**

Can we protect programs from each other without translation?

- Yes: Base and Bound!

- Used by, e.g., Cray-1 supercomputer

**Issues with Simple B&B Method**

Fragmentation problem over time

- Not every process is same size => memory becomes fragmented over time

Missing support for sparse address space

- Would like to have multiple chunks/program (Code, Data, Stack, Heap, etc)

Hard to do inter-process sharing

- Want to share code segments when possible

- Want to share memory between processes

- Helped by providing multiple segments per process

**More Flexible Segmentation**

Logical View: multiple separate segments

- Typical: Code, Data, Stack

- Others: memory sharing, etc

Each segment is given region of contiguous memory

- Has a base and limit

- Can reside anywhere in physical memory

**Implementation of Multi-Segment Model**

- Segment map resides in processor
  
  - Segment number mapped into base/limit pair
  
  - Base added to offset to generate physical address
  
  - Error check catches offset out of range

- As many chunks of physical memory as entires
  
  - Segment addressed by portion of virtual address
  
  - However, could be included in instruction instead:
    
    - x86 Example: mov [es:bx],ax.

**Intel x86 Special Registers**

Typical Segment Register

- Current Priority is RPL of Code Segment (CS)

Segmentation can't be just "turned off"

- What if we just want to use paging?

- Set base and bound to all of memory, in all segments

**Observations about Segmentation**

Translation on every instruction fetch, load or store

Virtual address space has holes

- Segmentation efficient for sparse address spaces

When it is OK to address outside valid range?

- This is how the stack (and heap?) allowed to grow

- For instance, stack takes fault, system automatically increases size of stack

Need protection mode in segment table

- For example, code segment would be read-only

- Data and stack would be read-write (stores allowed)

What must be saved/restored on context switch?

- Segment table stored in CPU, not in memory (small)

- Might store all of processes memory onto disk when switched (called "swapping")

**What if not all segments fit in memory?**

Extreme form of Context Switch: *Swapping*

- To make room for next process, some or all of the previous process is moved to disk
  
  - Likely need to send out complete segments

- This greatly increases the cost of context-switching

**What might be a desirable alternative?**

- Some way to keep only active portions of a process in memory at any one time

- Need finer granularity control over physical memory

**Problems with Segmentation**

- Must fit variable-sized chunks into physical memory

- May move processes multiple times to fit everything

- Limited options for swapping to disk

- Fragmentation: wasted space
  
  - External: free gaps between allocated chunks
  
  - Internal: don't need all memory within allocated chunks

**Paging: Physical Memory in Fixed Size Chunks**

Solution to fragmentation from segments?

- Allocate physical memory in fixed size chunks ("pages")

- Every chunk of physical memory is equivalent
  
  - Can use simple vector of bits to handle allocation:
    
    00110001110001101 ... 110010
  
  - Each bit represents page of physical memory
    
    1 => allocated, 0 => free

Should pages be as big as our previous segments?

- No: Can lead to lots of internal fragmentation
  
  - Typically have small pages (1K-16K)

- Consequently: need multiple pages/segment

**How to Implement Simple Paging?**

Page Table (One per process)

- Resides in physical memory

- Contains physical page and permission for each virtual page (e.g. Valid bits, Read, Write, etc)

Virtual address mapping

- Offset from Virtual address copied to Physical Address
  
  - Example: 10 bit offset => 1024-byte pages

- Virtual page # is all remaining bits
  
  - Example for 32-bits: 32-10 = 22 bits, i.e. 4 million entries
  
  - Physical page # copied from table into physical address

- Check Page Table bounds and permissions

**Where is page sharing used?**

The "kernel region" of every process has the same page table entries

- The process cannot access it at user level

- But on U->K switch, kernel code can access it AS WELL AS the region for THIS user
  
  - What does the kernel need to do to access other user processes?

- Different processes running same binary!
  
  - Execute-only, but do not need to duplicate code segments

- User-level system libraries (execute only)

- Shared-memory segments between different processes
  
  - Can actually share objects directly between processes
    
    - Must map page into same place in address space!
  
  - This is a limited form of the sharing that threads have within a single process

**Some simple security measures**

Address Space Randomization

- Position-Independent Code => can place user code anywhere in address space
  
  - Random start address makes much harder for attacker to cause jump to code that it seeks to take over

- Stack & Heap can start anywhere, so randomize placement

---

**How big do things get?**

32-bit address space => $2^{32}$ bytes (4 GB)

- Note: "b" = bit, and "B" = byte

- And for memory:
  
  - "K" (kilo) = $2^{10}$ = 1024 ≈ $10^3$ (But not quite!): Sometimes called "Ki" (Kibi)
  
  - "M" (mega) = $2^{20}$ = $(1024)^2$ = 1,048,576 ≈ $10^6$ (But not quite!): Sometimes called "Mi" (Mibi)
  
  - "G" (giga) = $2^{30}$ = $(1024)^3$ = 1,073,741,824 ≈ $10^9$ (But not quite!): Sometimes called "Gi" (Gibi)

Typical page size: 4 KB

- how many bits of the address is that ? (remember $2^{10}$ = 1024)

- Ans - 4KB = $4\times2^{10}$ = $2^{12}$ = 12 bits of the address

So how big is the simple page table for each process?

- $\frac{2^{32}}{2^{12}}=2^{20}$ (that's about a million entries) $\times4$ bytes each => 4 MB

- When 32-bit machines got started (vax 11/780, intel 80386), 16MB was a LOT of memory

How big is a simple page table on a 64-bit processor (x86_x64)?

- $\frac{2^{64}}{2^{12}}=2^{52}$ (that's $4.5\times10^{15}$ or 4.5 exa-entries) $\times8$ bytes each = $36\times10^{15}$ bytes or 36 exa-bytes! This is a ridiculous amount of memory!

- This is really a lot of space - for only the page table!

The address space is sparse, i.e. has holes that are not mapped to physical memory

- So, most of this space is taken up by page tables mapped to nothing

**Page Table**

What needs to be switched on a context switch?

- Page table pointer and limit

What provides protection here?

- Translation (per process) and dual-mode!

- Can't let process alter its own page table!

Analysis

- Pros
  
  - Simple memory allocation
  
  - Easy to share

- Con: What if address space is sparse?
  
  - E.g., on UNIX, code starts at 0, stack starts at ($2^{31}-1$)
  
  - With 1K pages, need 2 million page table entries!

- Con: What if table really big?
  
  - Not all pages used all the time => would be nice to have working set of page table in memory

Simple page table is way too big!

- Does it all need to be in memory?

- How about multi-level paging?

- or combining paging and segmentation

Page Table is a map (function) from VPN to PPN

> Virtual Address => Page Table => Physical Address

Simple page table corresponds to a very large lookup table

- VPN is index into table, each entry contains PPN

**What is in a Page Table Entry (PTE)?**

What is in a Page Table Entry (or PTE)?

- Pointer to next-level page table or to actual page

- Permission bits: valid, read-only, read-write, write-only

Example: Intel x86 architecture PTE:

- Address same format previous slide (10, 10, 12-bit offset)

- Intermediate page tables called "Directories"

**Multi-level Translation Analysis**

Pros:

- Only need to allocate as many page table entries as we need for application
  
  - In other wards, sparse address spaces are easy

- Easy memory allocation

- Easy Sharing
  
  - Share at segment or page level (need additional reference counting)

Cons:

- One pointer per page (typically 4K - 16K pages today)

- Page tables need to be contiguous
  
  - However, the 10b-10b-12b configuration keeps tables to exactly one page in size

- Two (or more, if >2 levels) lookups per reference
  
  - Seems very expensive!

**X86 Segment Descriptors (32-bit Protected Mode)**

Segments are implicit in the instruction (e.g. code segments) or part of the instruction

- There are 6 registers: SS, CS, DS, ES, FS, GS

What is in a segment register?

- A pointer to the actual segment description:

- G/L selects between GDT and LDT tables (global vs local descriptor tables)

- RPL: Requestor's Privilege Level (RPL of CS => Current Privilege Level)

Two registers: GDTR/LDTR hold pointers to global/local descriptor tables in memory

**How are segments used?**

One set of global segments (GDT) for everyone, different set of local segments (LDT) for every process

In legacy applications (16-bit mode):

- Segments provide protection for different components of user programs

- Separate segments for chunks of code, data, stacks
  
  - RPL of Code Segment => CPL (Current Privilege Level)

- Limited to 64K segments

Modern use in 32-bit mode:

- Even though there is full segment functionality, segments are set up as "flattened", i.e. every segment is 4GB in size

- One exception: Use of GS (or FS) as a pointer to "Thread Local Storage" (TLS)
  
  - A thread can make accesses to TLS like this:
    
    *mov eax, gs(0x0)*

Modern use in 64-bit ("long") mode

- Most segments (SS, CS, DS, ES) have zero base and no length limits

- Only FS and GS retain their functionality TLS

**Alternative: Inverted Page Table**

With all previous examples ("Forward Page Tables")

- Size of page table is at least as large as amount of virtual memory allocated to processes

- Physical memory may be much less
  
  - Much of process space may be out on disk or not in use

Answer: use a hash table

- Called an "Inverted Page Table"

- Size is independent of virtual address space

- Directly related to amount of physical memory

- Very attractive option for 64-bit address spaces
  
  - PowerPC, UltraSPARC, IA64

Cons:

- Complexity of managing hash chains: Often in hardware!

- Poor cache locality of page table

**Address Translation Comparison**

|                                         | Advantages                                                         | Disadvantages                                              |
|:---------------------------------------:|:------------------------------------------------------------------:|:----------------------------------------------------------:|
| Simple Segmentation                     | Fast context switching (segment map maintained by CPU)             | External fragmentation                                     |
| Paging (Single-Level)                   | No external fragmentation Fast and easy allocation                 | Large table size (~ virtual memory) Internal fragmentation |
| Paged Segmentation / Multi-Level Paging | Table size ~ # of pages in virtual memory Fast and easy allocation | Multiple memory references per page access                 |
| Inverted Page Table                     | Table size ~ # of pages in physical memory                         | Hash function more complex No cache locality of page table |

**Why Does Caching Help? Locality!**

- Temporal Locality (Locality in Time):
  
  - Keep recently accessed data items closer to processor

- Spatial Locality (Locality in Space):
  
  - Move contiguous blocks to the upper levels

**Translation Look-Aside Buffer**

Record recent Virtual Page # to Physical Frame # translation

If present, have the physical address without reading any of the page tables!

- Even if the translation involved multiple levels

- Caches the end-to-end result

Was invented by Sir Maurice Wilkes - prior to caches

- When you come up with a new concept, you get to name it!

- People realized "if it's good for page tables, why not the rest of the data in memory?"

On a TLB miss, the page tables may be cached, so only go to memory when both miss

**Sources of Cache Misses**

Compulsory (cold start or process migration, first reference): first access to a block

- "Cold" fact of life: not a whole lot you can do about it

- Note: If you are going to run "billions" of instruction, Compulsory Misses are insignificant

Capacity:

- Cache cannot contain all blocks access by the program

- Solution: increase cache size

Conflict (collision):

- Multiple memory locations mapped to the same cache location

- Solution 1: increase cache size

- Solution 2: increase associativity

**Physically-Indexed vs Virtually-Indexed Caches**

Physically-Indexed Caches

- Address handed to cache after translation

- Page Table holds physical addresses

- Benefits:
  
  - Every piece of data has single place in cache
  
  - Cache can stay unchanged on context switch

- Challenges:
  
  - TLB is in critical path of lookup!

- Pretty Common today (e.g. x86 processors)

Virtually-Indexed Caches

- Address handed to cache before translation

- Page Table holds virtual addresses (one option)

- Benefits:
  
  - TLB not in critical path of lookup, so can be faster

- Challenges:
  
  - Same data could be mapped in multiple places 
  
  - May need to flush cache on context switch

**TLB organization: include protection**

How ig does TLB actually have to be?

- Usually small: 128-512 entries (larger now)

- Not very big, can support higher associativity

Small TLBs usually organized as fully-associative cache

- Lookup is by Virtual Address

- Returns Physical Address + other info

What happens when fully-associative is too slow?

- Put a small (4-16 entry) direct-mapped cache in front

- Called a "TLB Slice"

Example for MIPS R3000:

| Virtual Address | Physical Address | Dirty | Ref | Valid | Access | ASID |
|:---------------:|:----------------:|:-----:|:---:|:-----:|:------:|:----:|
| 0xFA00          | 0x0003           | Y     | N   | Y     | R/W    | 34   |
| 0x0040          | 0x0010           | N     | Y   | Y     | R      | 0    |
| 0x0041          | 0x0011           | N     | Y   | Y     | R      | 0    |

**Reducing translation time for physically-indexed caches**

As described, TLB lookup is in serial with cache lookup

- Consequently, speed of TLB can impact speed of access to cache

Machines with TLBs go one step further:

overlap TLB lookup with cache access

- Works because offset available early

- Offset in virtual address exactly covers the "cache index" and "byte select"

- Thus can select the cached byte(s) in parallel to perform address translation 

**What happens on a Context Switch?**

Need to do something, since TLBs map virtual addresses to physical addresses

- Address Space just changed, so TLB entries no longer valid!

Options?

- Invalidate TLB: simple but might be expensive
  
  - What if switching frequently between processes?

- Include ProcessID in TLB
  
  - This is an architectural solution: needs hardware

What if translation tables change?

- For example, to move page from memory to disk or vice versa...

- Must invalidate TLB entry!
  
  - Otherwise, might think that page is still in memory!

- Called "TLB Consistency"

Aside: with Virtually-Indexed cache, need to flush cache!

**Page Fault**

The Virtual-to-Physical Translation fails

- PTE marked invalid, Priv. Level Violation, Access violation, or does not exist

- Causes an Fault / Trap
  
  - Not an interrupt because synchronous to instruction execution

- May occur on instruction fetch or data access

- Protection violations typically terminate the instruction

Other Page Faults engage operating system to fix the situation and retry the instruction

- Allocate an additional stack page or

- Make the page accessible - Copy on Write,

- Bring page in from secondary storage to memory - demand paging

Fundamental inversion of the hardware / software boundary

**Demand Paging**

Modern programs require a lot of physical memory

- Memory per system growing faster than 25%-30% per year

But they don't use all their memory all of the time

- 90-10 rule: programs spend 90% of their time in 10% of their code

- Wasteful to require all of user's code to be in memory

Solution: use main memory as "cache" for disk

**Demand Paging as Caching, ...**

What "block size"? - 1 page (e.g, 4 KB)

What "organization" i.e. direct-mapped, set-assoc., fully-associative?

- Fully associative since arbitrary virtual → physical mapping

How do we locate a page?

- First check TLB, then page-table traversal

What is page replacement policy? (i.e. LRU, Random...)

- This requires more explanation... (kinda LRU)

What happens on a miss?

- Go to lower level to fill miss (i.e. disk)

What happens on a write? (write-through, write back)

- Definitely write-back - need dirty bit!

**Illusion of Infinite Memory**

Disk is larger than physical memory =>

- In-use virtual memory can be bigger than physical memory

- Combined memory of running processes much larger than physical memory
  
  - More programs fit into memory, allowing more concurrency

Principle: Transparent Level of Indirection (page table)

- Supports flexible placement of physical data
  
  - Data could be on disk or somewhere across network

- Variable location of data transparent to user program
  
  - Performance issue, not correctness issue

**Demand Paging Mechanisms**

PTE makes demand paging implementable

- Valid => Page in memory, PTE points at physical page

- Not Valid => Page not in memory; use info in PTE to find it on disk when necessary

Suppose user references page with invalid PTE?

- Memory Management Unit (MMU) traps to OS
  
  - Resulting trap is a "Page Fault"

- What does OS do on a Page Fault?
  
  - Choose an old page to replace
  
  - If old page modified ("D=1"), write contents back to disk
  
  - Change its PTE and any cached TLB to be invalid
  
  - Load new page into memory from disk
  
  - Update page table entry, invalidate TLB for new entry
  
  - Continue thread from original faulting location

- TLB for new page will be loaded when thread continued!

- While pulling pages off disk for one process, OS runs another process from ready queue
  
  - Suspended process sits on wait queue

**Many Uses of Virtual Memory and "Demand Paging"...**

Extend the stack

- Allocate a page and zero it

Extend the heap (sbrk of old, today mmap)

Process Fork

- Create a copy of the page table

- Entries refer to parent pages - NO-WRITE

- Shared read-only pages remain shared

- Copy page on write

Exec

- Only bring in parts of the binary in active use

- Do this on demand

MMAP to explicitly share region (or to access a file as RAM)

**Classic: Loading an executable into memory**

.exe

- lives on disk in the file system

- contains contents of code & data segments, relocation entries and symbols

- OS loads it into memory, initializes registers (and initial stack pointer)

- program sets up stack and heap upon initialization

**Create Virtual Address Space of the Process**

Utilized pages in the VAS are backed by a page block on disk

- Called the backing store or swap file

- Typically in an optimized block store, but can think of it like a file

**Provide Backing Store for VAS**

- User Page table maps entire VAS

- Resident pages mapped to memory frames

- For all other pages, OS must record where to find them on disk

**What Data Structure Maps Non-Resident Pages to Disk?**

- FindBlock(PID, page#) → disk_block
  
  - Some OSs utilize spare space in PTE for paged blocks
  
  - Like the PT, but purely software

- Where to store it?
  
  - In memory - can be compact representation if swap storage is contiguous on disk
  
  - Could use hash table (like Inverted PT)

- Usually want backing store for resident pages too

- May map code segment directly to on-disk image
  
  - Saves a copy of code to swap file

- May share code segment with multiple instances of the program

---

During a page fault, where does the OS get a free frame?

- Keeps a free list

- Unix runs a "reaper" if memory gets too full
  
  - Schedule dirty pages to be written back on disk
  
  - Zero (clean) pages which haven't been accessed in a while

- As a last resort, evict a dirty page first

How can we organize these mechanisms?

- Work on the replacement policy

How many page frames/process?

- Like thread scheduling, need to "schedule" memory resources:
  
  - Utilization? fairness? priority?

- Allocation of disk paging bandwidth

**Working Set Model**

As a program executes it transitions through a sequence of "working sets" consisting of varying sized subsets of the address space

**Cache Behavior under WS model**

- Amortized by fraction of time the Working Set is active

- Transitions from one WS to the next

- Capacity, Conflict, Compulsory misses

**Another model of Locality: Zipf**

Likelihood of accessing item of rank $r$ is $\alpha$ $\frac{1}{r^a}$

Although rare to access items below the top few, there are so many that it yields a "heavy tailed" distribution

Substantial value from even a tiny cache

Substantial misses from even a very large cache

**Demand Paging Cost Model**

Since Demand Paging like caching, can compute average access time!

("Effective Access Time")

- $\text{EAT} = \text{Hit Rate} \times \text{Hit Time} + \text{Miss  Rate} \times \text{Miss Time}$

- $\text{EAT} = \text{Hit Time} + \text{Miss Rate} \times \text{Miss Penalty}$

Example:

- Memory access time = 200 nanoseconds

- Average page-fault service time = 8 milliseconds

- Suppose p = Probability of miss, 1-p = Probably of hit

- Then, we can compute EAT as follows:
  
  $EAT = 200ns+p\times 8\,\text{ms}=200ns+p\times8,000,000\,\text{ns}$

If one access out of 1,000 causes a page fault, then $EAT=8.2\,\mu s$:

- This is a slowdown by a factor of 40!

What if want slowdown by less than 10%?

- $\text{EAT}<200\text{ns}\times1.1\Rightarrow p<2.5\times10^{-6}$

- This is about 1 page fault in 400,000!

**What Factors Lead to Misses in Page Cache?**

Compulsory Misses:

- Pages that have never been paged into memory before

- How might we remove these misses?
  
  - Prefetching: loading them into memory before needed
  
  - Need to predict future somehow!

Capacity Misses:

- Not enough memory. Must somehow increase available memory size.

- Can we do this?
  
  - One option: Increase amount of DRAM (not quick fix!)
  
  - Another option: If multiple processes in memory: adjust percentage of memory allocated to each one!

Conflict Misses:

- Technically, conflict misses don't exist in virtual memory, since it is a "fully-associative" cache

Policys Misses:

- Caused when pages were in memory, but kicked out prematurely because of the replacement policy

**Page Replacement Policies**

Why do we care about Replacement Policy?

- Replacement is an issue with any cache

- Particularly important with pages
  
  - The cost of being wrong is high: must go to disk
  
  - Must keep important pages in memory, not toss them out

FIFO (First In, First Out)

- Throw out oldest page. Be fair - let every page live in memory for same amount of time.

- Bad - throws out heavily used pages instead of infrequently used

RANDOM:

- Pick random page for every replacement

- Typical solution for TLB's. Simple hardware

- Pretty unpredictable - makes it hard to make real-time guarantees

MIN (Minimum):

- Replace page that won't be used for the longest time

- Great (provably optimal), but can't really know future...

- But past is a good predictor of the future...

**Replacement Policies (Con't)**

LRU (Least Recently Used):

- Replace page that hasn't been used for the longest time

- Programs have locality, so if something not used for a while, unlikely to be used in the near future.

- Seems like LRU should be a good approxiamation to MIN.

How to implement LRU? Use a list:

- On each use, remove page from list and place at head

- LRU page is at tail

Problems with this scheme for paging?

- Need to know immediately when page used so that can change position in list...

- Many instructions for each hardware access

**Approximating LRU: Clock Algorithm**

Clock Algorithm: Arrange physical pages in circle with single clock hand

- Approximate LRU (approximation to approximation to MIN)

- Replace an old page, not the oldest page

Details:

- Hardware "use" bit per physical page (called "accessed" in Intel architecture):
  
  - Hardware sets use bit on each reference
  
  - If use bit isn't set, means not referenced in a long time
  
  - Some hardware sets use bit in the TLB; must be copied back to page TLB entry gets replaced

- On page fault:
  
  - Advance clock hand (not real time)
  
  - Check use bit:
    
    - 1 → used recently; clear and leave alone
    
    - 0 → selected candidate for replacement

Will always find a page or loop forever?

- Even if all use bits set, will eventually loop all the way around $\Rightarrow$ FIFO

What if hand moving slowly?

- Good sign or bad sign?
  
  - Not many page faults
  
  - or find page quickly

What if hand is moving quickly?

- Lots of page faults and/or lots of reference bits set

One way to view clock algorithm:

- Crude partitioning of pages into two groups: young and old

**$N^{th}$ Chance version of Clock Algorithm**

$N^{th}$ chance algorithm: Give page N chances

- OS keeps counter per page: # sweeps

- On page fault, OS checks use bit:
  
  - 1 $\to$ clear use and also clear counter (used in last sweep)
  
  - 0 $\to$ increment counter; if count=N, replace page

- Means that clock hand has to sweep by N times without page being used before page is replaced

How do we pick N?

- Why pick large N? Better approximation to LRU
  
  - If N ~ 1K, really good approximation

- Why pick small N? More efficient
  
  - Otherwise might have to look a long way to find free page

What about "modified" (or "dirty") pages?

- Takes extra overhead to replace a dirty page, so give dirty pages an extra chance before replacing?

- Common approach:
  
  - Clean pages, use N=1
  
  - Dirty pages, use N=2 (and write back to disk when N=1)

**Clock Algorithms Variations**

Do we really need hardware-supported "modified" bit?

- No. Can emulate it using read-only bit
  
  - Need software DB of which pages are allowed to be written (needed this anyway)
  
  - We will tell MMU that pages have more restricted permissions than the actually do to force page faults (and allow us notice when page is written)

- Algorithm (Clock-Emulated-M):
  
  - Initially, mark all pages as read-only (W$\to$0), even writable data pages. Further, clear all software versions of the "modified" bit $\to$ 0 (page not dirty)
  
  - Writes will cause a page fault, Assuming write is allowed, OS sets software "modified" bit $\to$ 1, and marks page as writable (W$\to$1).
  
  - Whenever page written back to disk, clear "modified" bit $\to$ 0, mark read-only

Do we really need a hardware-supported "use" bit?

- No. Can emulate it similar to above (e.g. for read operation)
  
  - Kernel keeps a "use" bit and "modified" bit for each page

- Algorithm (Clock-Emulated-Use-and-M):
  
  - Mark all pages as invalid, even if in memory.
    
    Clear emulated "use" bits $\to$ 0 and "modified" bits $\to$ 0 for all pages (not used, not dirty)
  
  - Read or write to invalid page traps to OS to tell use page has been used
  
  - OS sets "use" bit $\to$ 1 in software to indicate that page has been "used".
    
    Further:
    
    - If read, mark page as read-only, W $\to$ 0 (will catch future writes)
    
    - If write (and write allowed), set "modified" bit $\to$ 1, mark page as writable (W $\to$ 1)
  
  - When clock hand passes, reset emulated "use" bit $\to$ 0 and mark page as invalid again
  
  - Note that "modified" bit left alone until page written back to disk

Remember, however, clock is just an approximation of LRU!

- Can we do a better approximation, given that we have to take page faults on some reads and writes to collect use information?

- Need to identify an old page, not oldest page!

- Answer: second chance list

**Second-Chance List Algorithm (VAX/VMS)**

- Split memory in two: Active list (RW), SC list (Invalid)

- Access pages in Active list at full speed

- Otherwise, Page Fault
  
  - Always move overflow page from end of Active list to front of Second-chance list (SC) and mark invalid
  
  - Desired Page On SC List: move to front of Active list, mark RW
  
  - Not on SC list: page in to front of Active list, mark RW; page out LRU victim at end of SC list

How many pages for second chance list?

- If 0 $\Rightarrow$ FIFO

- If all $\Rightarrow$ LRU, but page fault on every page reference

Pick intermediate value. Result is:

- Pro: Few disk accesses (page only goes to disk if unused for a long time)

- Con: Increased overhead trapping to OS (software / hardware tradeoff)

With page translation, we can adapt to any kind of access the program makes

- Later, we will show how to use page translation / protection to share memory between threads on widely separated machines

**Transactions**

Closely related to critical sections for manipulating shared data structures

They extend concept of atomic update from memory to stable storage

- Atomically update multiple persistent data structures

Many ad-hoc approaches

- FFS carefully ordered the sequence of updates so that if a crash occurred while manipulating directory or inodes the disk scan on reboot would detect and recover the error (fsck)

- Applications use temporary files and rename

**Concept of a log**

One simple action is atomic - write/append a basic item

Use that to seal the commitment to a whole series of actions

**Transactional File Systems**

Better reliability through use of log

- Changes are treated as transactions

- A transaction is committed once it is written to the log
  
  - Data forced to disk for reliability
  
  - Process can be accelerated with NVRAM

- Although File system may not be updated immediately, data preserved in the log

Difference between "Log Structured" and "Journaled"

- In a Log Structured filesystem, data stays in log form

- In a Journaled filesystem, Log used for recovery

**Journaling File Systems**

Don't modify data structures on disk directly

Write each update as transaction recorded in a log

- Commonly called a journal or intention list

- Also maintained on disk (allocate blocks for it when formatting)

Once changes are in the log, they can be safely applied to file system

- e.g. modify inode pointers and directory mapping

Garbage collection: once a change is applied, remove its entry from the log

Linux took original FFS-like file system (ext2) and added a journal to get ext3!

- Some options: whether or not to write all data to journal or just metadata

Other examples: NTFS, Apple HFS+, Linux XFS, JFS, ext4

**Journaling Summary**

Why go through all this trouble?

- Updates atomic, even if we crash:
  
  - Update either gets fully applied or discarded
  
  - All physical operations *treated as a logical unit*

Isn't this expensive?

- Yes! We're now writing all data twice (once to log, once to actual data blocks in target file)

- Modern filesystems journal metadata updates only
  
  - Record modifications to file system data structures
  
  - But apply updates to a file's contents directly

**The Log Structured File System (LFS)**

Log Structured File System:

- The LOG IS the storage

Log: One continuous sequence of blocks that wrap around whole disk

- Inodes put into log when changed and point to new data in the log

Simple example:

- Create two new files:
  
  - dir1/file1 and dir2/file2
  
  - Must write new data blocks for files and for new information in directories

- LFS writes everything sequentially

- Unix FFS requires 10 non-sequential writes (inodes written twice for ease of recovery)

The log IS what is recorded on disk

- File system operations logically replay log to get result

- Create data structures to make this fast

- On recovery, replay the log

Index (inodes) and directories are written into the log too

Large, important portion of the log is cached in memory

- Relies on Buffer Cache to make reading fast

Do everything in bulk: log is collection of large segments

Each segment contains a summary of all the operations within the segment

- Fast to determine if segment is relevant or not

Free space is approached as continual cleaning process of segments

- Detect what is live or not within a segment

- Copy live portion to new segment being formed (replay)

- Garbage collection entire segment

- No bit map

**Flash Filesystems**

Cannot overwrite pages!

- Must move contents to an erased page

- Small changes $\Rightarrow$ lots of rewriting of data/wear out!

Program/Erase (PE) Wear

- Permanent damage to gate oxide at each flash cell

- Caused by high program/erase voltages

- Issues: trapped charges, premature leakage of charge

- *Need to balance how frequently cells written: "Wear Leveling"*

Flash Translation Layer (FTL)

- Translates between Logical Block Addresses (at OS level) and Physical Flash Page Addresses

- Manages the wear and erasure state of blocks and pages

- Tracks which blocks are garbage but not erased

Management Process (Firmware)

- Keep freelist full, Manage mapping,

- Track wear state of pages

**Centralized vs Distributed Systems**

Centralized System: major functions performed by a single physical computer

- Originally, everything on single computer

- Later: client/server model

Distributed System: physically separate computers working together on task

- Early model: multiple servers working together
  
  - Probably in the same room or building
  
  - Often called a "cluster"

- Later models: peer-to-peer/wide-spread collaboration

Why do we want distributed systems?

- Cheaper and easier to build lots of simple computers

- Easier to add power incrementally

- Users can have complete control over some components

- Collaboration: much easier for users to collaborate through network resources (such as network file systems)

The promise of distribute systems:

- Higher availability: one machine goes down, use another

- Better durability: store data in multiple locations

- More security: each piece easier to make secure

**Distributed Systems: Reality**

Reality has been disappointing

- *Worse availability*: depend on every machine being up
  
  - Lamport: "*A distributed system is one in which the failure of a computer you didn't even know existed can render your own computer unusable*."

- *Worse reliability*: can lose data if any machine crashes

- *Worse security*: anyone in world can break into system

Coordination is more difficult

- Must coordinate multiple copies of shared state information

- What would be easy in a centralized system becomes a lot more difficult

Trust/Security/Privacy/Denial of Service

- Many new variants of problems arise as a result of distribution

- Can you trust the other members of a distributed application enough to even perform a protocol correctly?

- Corollary of Lamport's quote: "A distributed system is one where you can't do work because some computer you didn't even know existed is successfully coordinating an attack on my system!"

**Distributed Systems: Goals/Requirements**

- *Transparency*: the ability of the system to mask its complexity behind a simple interface

- Possible transparencies:
  
  - *Location*: Can't tell where resources are located
  
  - *Migration*: Resources may move without the user knowing
  
  - *Replication*: Can't tell how many copies of resource exist
  
  - *Concurrency*: Can't tell how many users there are
  
  - *Parallelism*: System may speed up large jobs by splitting them into smaller pieces
  
  - *Fault Tolerance*: System may hide various things that go wrong

- Transparency and collaboration require some way for different processors to communicate with one another

**How do entities communicate? A Protocol!**

A protocol is an agreement on how to communicate, including:

- Syntax: how a communication is specified & structured
  
  - Format, order messages are sent and received

- Semantics: what a communication means
  
  - Actions taken when transmitting, receiving, or when a timer expires

Described formally by a state machine

- Often represented as a message transaction diagram

- Can be a partitioned state machine: two parties synchronizing duplicate sub-state machines between them

**Moderate Interpretation**

Think twice before implementing functionality in the network

If hosts can implement functionality correctly, implement it in a lower layer only as a performance enhancement

But do so only if it does not impose burden on applications that do not require that functionality

This is the interpretation we are using

---

**Virtual Filesystem Switch**

VFS: Virtual abstraction similar to local file system

- Provides virtual superblocks, inodes, files, etc

- Compatible with a variety of local and remote file systems
  
  - provides object-oriented way of implementing file systems

VFS allows the same system call interface (the API) to be used for different types of file systems

- The API is to the VFS interface rather than any specific type of file system

**VFS Common File Model in Linux**

Four primary object types for VFS:

- superblock object: represents a specific mounted filesystem

- inode object: represents a specific file

- dentry object: represents a directory entry

- file object: represents open file associated with process

There is no specific directory object (VFS treats directories as files)

May need to fit the model by faking it

- Example: make it look like directories are files

- Example: make it look like have inodes, superblocks, etc.

**Stateless Protocol**

Stateless Protocol: A protocol in which all information required to service a request is included with the request

Even better: Idempotent Operations - repeating an operation multiple times is same as executing it just once (e.g., storing to a mem addr.)

**Network File System (NFS)**

Three Layers for NFS system

- UNIX file-system interface: open, read, write, close calls + file descriptors

- VFS layer: distinguishes local from remote files
  
  - Calls the NFS protocol procedures for remote requests

- NFS service layer: bottom layer of the architecture
  
  - Implements the NFS protocol

NFS Protocol: RPC for file operations on server

- XDR Serialization standard for data format independence

- Reading/searching a directory

- manipulating links and directories

- accessing file attributes/reading and writing files

Write-through caching: Modified data committed to server's disk before results are returned to the client

- lose some of the advantages of caching

- time to perform write() can be long

- Need some mechanism for readers to eventually notice changes!

NFS servers are stateless; each request provides all arguments require for execution

Idempotent: Performing requests multiple times has same effect as performing them exactly once

Failure Model: Transparent to client system

**NFS Cache consistency**

NFS protocol: weak consistency

- Client polls server periodically to check for changes
  
  - Polls server if data hasn't been checked in last 3-30 seconds (exact timeout it tunable parameter).
  
  - Thus, when file is changed on one client, server is notified, but other clients use old version of file until timeout.

NFS Pros:

- Simple, Highly portable

NFS Cons:

- Sometimes inconsistent!

- Doesn't scale to large # clients
  
  - Must keep checking to see if caches out of date
  
  - Server becomes bottleneck due to polling traffic

**Andrew File System**

Andrew File System (AFS, late 80's) $\to$ DCE DFS (commercial product)

Callbacks: Server records who has copy of file

- On changes, server immediately tells all with old copy

- No polling bandwidth (continuous checking) needed

Write through on close

- Changes not propagated to server until close()

- Session semantics: updates visible to other clients only after the file is closed
  
  - As a result, do not get partial writes: all or nothing!
  
  - Although, for processes on local machine, updates visible immediately to other programs who have file open

In AFS, everyone who has file open sees old version

- Don't get newer versions until reopen file

Data cached on local disk of client as well as memory

- On open with a cache miss (file not on local disk):
  
  - Get file from server, set up callback with server

- On write followed by close:
  
  - Send copy to server; tells all clients with copies to fetch new version from server on next open (using callbacks)

What if server crashes? Lose all callback state!

- Reconstruct callback information from client: go ask everyone "who has which files cached?"

AFS Pro: Relative to NFS, less server load:

- Disk as cache $\Rightarrow$ more files can be cached locally

- Callbacks $\Rightarrow$ server not involved if file is read-only

For both AFS and NFS: central server is bottleneck!

- Performance: all writes$\to$server, cache misses$\to$server

- Availability: Server is single point of failure

- Cost: server machine's high cost relative to workstation
