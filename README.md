# Operating System Summary

![Bidur Sapkota](https://www.bidursapkota.com.np/_next/image?url=%2Fimages%2Fprofile3.png&w=48&q=75 "Bidur Sapkota - Developer")&nbsp;[Bidur Sapkota](https://www.bidursapkota.com.np/)

![Operating System Summary by Bidur Sapkota](/test.png "Operating System Summary – Blog by Bidur Sapkota")

## Table of Contents

1. [Unit 1: Introduction](#introduction)
2. [Unit 2: Process Management](#process-management)

## Introduction

**Operating System**

- OS is software that manages the computer hardware as well as providing an environment for application programs to run.
- Provides abstraction, simple interface to complex hardware. (OS as extension machine / abstraction provider)
- Allocates processors, memories, and I/O devices among various programs. (OS as resource manager)

**Shell**

- Provides Text Interface
- Translates commands into a form that kernel can understand

**Kernel**

- Core component of OS that coordinates necessary resources & performs requested operations.

---

**Evolution of OS**

**First Generation**

- Physically wired programs, no OS

**Second Generation**

- Batch Processing OS

**Third Generation**

- Multiprogramming OS, Time Sharing OS

**Fourth Generation**

- GUI based OS, Bundled for many PC hardware

**Fifth Generation**

- OS for handheld Phones

---

**Types of OS**

**Batch OS**

- handles groups of similar, repetitive jobs

**Multi-Programming OS**

- Multiple programs stay in memory, and the CPU switches to another program whenever one performs I/O.

**Multi-Tasking OS**

- CPU executes multiple tasks by switching between them.

**Multi-Processing OS**

- More than one processor executing multiple processes parallelly

**Distributed OS**

- Multiple computers communicate over a network to function as a single system, enhancing scalability and reliability.

**Real-Time OS**

- Designed for processing task with time constraints

---

**OS components**

**Process Management System**

- creating, deleting, pausing, resuming, scheduling, and coordinating processes and their resources.

**Memory Management System**

- allocating memory, managing virtual memory, and moving data between RAM and disk

**Secondary Storage Management**

- allocating space, reclaiming space, avoiding fragmentation, assigning storage to files, and scheduling disk operations

**File Management System**

- organizing files in directories, managing paths and logical blocks, and creating, deleting, opening, reading, and writing files

**I/O System**

- handling I/O requests, using device drivers, managing buffers, and supporting busy waiting, interrupts, and DMA

**Protection and Security System**

- controlling access to resources, enforcing permissions, isolating processes, and preventing unauthorized use

---

**OS Structures**

**Monolithic Systems:**

- single large kernel, all services inside, fast direct calls, hard to manage, one failure can crash whole system

**Layered Systems:**

- OS divided into layers, each depends on the one below, easier debugging, more overhead of passing info throughout layers

**Microkernels:**

- minimal kernel, services in user space, safer and modular, uses message passing, slower due to communication overhead

**Modular Structure:**

- small core kernel with loadable modules, easy to extend/replace, simpler debugging, added complexity and slight overhead

**Client-Server Model:**

- client process requests services from server process via message passing, can run locally or over network, often built on a microkernel

**Virtual Machines:**

- hypervisor creates isolated virtual systems, multiple OS share hardware, flexible but limited by physical resource capacity

**Exokernels:**

- kernel only handles protection/allocation, gives apps direct hardware access, no forced abstractions, extremely minimal and flexible

---

**System Calls:**

- interface for programs to request OS services (process, memory, files, devices, protection, networking)
- eg: fork(), read(), getpid(), pipe(), chmod()

**Example (read):**

- read(fd, buffer, nbytes) returns actual bytes read

---

**Examples of OS**

- UNIX, Linux, Windows, Embedded, Android, iOS

---

## Process Management

**Process**

- program in execution
- needs CPU time, memory, files, and I/O devices

**Two-State Process Model**

- Running, Not Running

**Five-State Process Model**

- NEW, READY, RUNNING, WAITING, TERMINATED

**Process Control Block (PCB)**

- OS data structure that stores all process information
- enables process control, suspension, resumption, and context switching

**Components of PCB**

- PID, Process State, Priority, Accounting Info, Program Counter, CPU Registers, PCB Pointers, Open Files List, I/O Status Info

**Context Switching**

- saving current process state to PCB and loading next process state
- stores PC, registers, and execution context
- loads PCB and resumes process from last instruction

**Thread**

- single execution sequence within a process that shares memory and resources with other threads but has its own program counter, registers, and stack, enabling faster creation and context switching than processes.

**Multithreading**

- multiple threads execute concurrently in one program
- improves performance and responsiveness

**User-Level Threads**

- managed by thread library, not kernel
- fast thread operations (no system calls)
- OS treats process as single-threaded
- blocking system call blocks entire process
- no true parallelism

**Kernel-Level Threads**

- managed and scheduled by kernel
- blocking one thread doesn’t block others
- true parallelism on multiprocessors

**Thread Mapping Models**

**Many-to-One:**

- many user threads → one kernel thread
- no parallelism, blocking affects all threads

**One-to-One:**

- one user thread → one kernel thread
- true parallelism, higher overhead

**Many-to-Many:**

- many user threads → many kernel threads
- flexible, efficient, balanced concurrency

---

### **Process Scheduling**

- selecting which ready process runs on CPU
- maximizes CPU utilization and throughput
- ensures fairness and low response time

---

### **Schedulers**

**Long-Term Scheduler:**

- selects processes from disk to memory
- controls degree of multiprogramming
- balances CPU-bound and I/O-bound jobs

**Medium-Term Scheduler:**

- swaps processes out/in of memory
- reduces memory load (only active process in memory)

**Short-Term Scheduler:**

- selects next process from ready queue
- runs very frequently

---

### **Dispatcher**

- transfers CPU control to selected process
- performs context switching
- loads process state from PCB

---

### **Scheduling Criteria**

- **CPU utilization:** keep CPU busy
- **Throughput:** processes completed per unit time
- **Turnaround time:** submission → completion
- **Waiting time:** time spent in ready queue
- **Response time:** submission → first response
- **Fairness:** equal CPU share, avoid starvation

---

### **Scheduling Goals**

- fair CPU allocation (all systems)
- maximize job completion rate (batch)
- minimize turnaround time (batch)
- minimize response time (interactive)
- meet deadlines (real-time)

---

### **Preemptive Scheduling**

- OS can interrupt running process
- higher-priority process can preempt
- improves responsiveness
- causes context-switch overhead
- possible starvation

---

### **Non-Preemptive Scheduling**

- process runs until completion or blocking
- simpler and lower overhead
- poor response time
- long processes may monopolize CPU

---

### **FCFS Scheduling**

- processes execute in arrival order
- non-preemptive
- simple queue implementation
- long average waiting time

---

### **Shortest Job First (SJF)**

- shortest execution time runs first
- optimal average waiting time
- non-preemptive
- needs execution time prediction
- starvation of long jobs possible

---

### **Shortest Remaining Time First (SRTF)**

- preemptive version of SJF
- process with least remaining time runs
- better response time
- high context switching overhead
- long processes may starve
