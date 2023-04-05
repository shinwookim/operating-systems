# What Is an Operating System?
> An operating system is a piece of software that manages resources and abstracts details

A modern computer is a complex system that consists of a processor (sometimes multiple processors), main memory (such a RAM), disks (HDDs and SSDs), and other peripherals (such as a mouse, network interface, or a printer) which all interact with one another. Because there are so many components, effectively managing and using each to their potential is a daunting task. Hence, most computers are equipped with a software called an **operating system** which serves two tasks:
1. Manage resources
2. Abstract details

These two primary functions provide us with a basic definition of an operating system. Still, our definition is rather crude and vague. It tells us what the operating system *does*, but not what the operating system *is*. Throughout our studies, we will look at more supplementing definitions which will reveal what an operating system is. However, for now, it will suffice at driving our understanding.

## Managing Resources
Our primitive definition claims that an operating system is a piece of software which *manages resources*. However, before we can study how the operating system does this, we must first examine what a **resource** is. Broadly speaking, a resource is something of finite quantity—the word *finite* is used not in reference to its mathematical definition but to mean that it is *reasonably constrained*—that is needed by the computer to conduct tasks. That is, our computer system is restricted in its capacity to carry out its tasks by the quantity of resources.

### CPU Time
One of the most important, yet neglected, resource in a computer is **CPU Time**. CPU time is finite in that, given a fixed unit of time, there are only a limited number of instructions that can be run. Hence, due to this fixed number of instructions, the ability of the computer to conduct tasks (run programs) is restricted. We will see later how we can optimally manage the CPU time when we talk about [[04 Scheduling]].

### Memory
Another common resource in a computer system is **memory**. Recall that most modern computers are built around the [Von Neumann architecture](https://en.wikipedia.org/wiki/Von_Neumann_architecture), which states that the code and data of all programs must live in main memory. As a consequence of this fact, the capacity of memory restricts how many instructions can be loaded, and then fetched by the CPU. Hence, the capacity of our memory restricts the ability of the computer to conduct tasks. We will see how to optimally manage memory usage when we talk about [[07 Memory Management]].

#### Von Neumann Architecture
As an aside, the distinction between *code* and *data* is quite minimal in the Von Neumann architecture. Since both are RAM residents, it is possible to run a program which modifies its own code as it runs (although this is highly discouraged). In comparison, the [Harvard architecture](https://en.wikipedia.org/wiki/Harvard_architecture) has two separate memories (one for data and the other for code) and does not allow this.

While most computer systems largely follow the Von Neumann architecture, there is an argument that modern CPUs also implement the Harvard architecture. This is because modern CPUs possesses a split L1 cache (storing code and data separately). In fact, it may be even arguable to say that a modern system can change between either architecture depending on what the focus is on and what memory the system is accessing.

### I/O Devices
**Input/Output devices** are another example of a system resource. Since memory capacity is limited (and expanding it too costly), we often store data that is currently not in use to I/O devices such as disks and file systems. Because all program executables are stored on disks prior to running, the devices clearly restrict our capacity to run programs. Furthermore, some programs may depend on other I/O devices such as network interfaces, which slows down our program and further restricting our system.

### Security
**Security** is a concept that is heavily intertwined with the management and protection of resources. Since the operating system is responsible for managing resources, it is a great place to implement security (for instance, access control). Throughout our studies of the operating system, we will see various methods and implementations that allow for a better security of our computers. We will often ask questions such as “*Even if you can physically access resource X, should you be allowed to do it?,*” and explore the topics of *security* and *availability*. 

## Abstracting Details
In the early days of computing, resources such as *RAM capacity* and *CPU speed* were so limited that we could only run one program at a time. During this time, resource management was trivial since we could give the program exclusive access to the entirety of the system resources.

However, as resources became more abundant (and computers much faster), users wanted to be able to run multiple programs simultaneously. To do so, computer scientists had to devise a way to share resources among various processes. For example, since the Von Neumann architecture forces the program’s code to be loaded into memory, to run multiple programs we need a way to share the memory among the processes.

Sharing is challenging because there is a limited amount of resources and each process is greedy. We have enough resources that sharing is possible, but not enough that each process can receive everything it needs. If our resources were extremely plentiful (to the point that it was close to being unbounded), we would simply give out everything that each program's requests and resource management would be trivial.

Furthermore, we don't want programs taking over resources held by other programs. A developer designing a program should not have to worry about other programs running concurrently taking over resources. To make the programmer's job easier, we can abstract a notion of **exclusive access** to the resources. By providing an interface where a program seemingly have exclusive access to the resource, the programmer can forgo their worries about the presence of other processes, instead focusing only on the abundance of resources (whether the resource is available or not). As an added benefit, we have also ensured a semblance of security since with exclusive access a program cannot access the resource (for example data) of another program. Typically, these abstractions are provided via **virtualization**.

# Types of Operating Systems
An operating system exists because there are multiple processes competing for the same limited resource. However, some systems have more resources (and more demand) than others. Hence, depending on how much resource a system has, there are different types of operating systems that mange it.
| Many Resources             | Limited Resources (Smaller Systems) |
| -------------------------- | ----------------------------------- |
| Mainframe OS               | Real-Time OS                        |
| Server OS & Supercomputers | Embedded OS                         |
| Parallel Computer OS       | Smart Card OS                       |
| Personal Computer OS                           |                                     |

## Systems with Many Resources
When we typically hear computers, we often think about the personal computers with lots of resources (such as desktop PCs, smartphones, etc.). These computers will be our primary focus as they have enough resources that sharing is possible, but not trivial.

However, there are systems with much larger amount of resources. One example is a *mainframe computer*. A mainframe is a type of computer that has enough resources to virtualize an entire computer (*Virtual Machines* are one of the oldest operating systems). With the amount of resources they have, resource management is almost trivial.

## Systems with Limited Resources
Although we will primarily focus on operating systems for computers with many resources, it is important to recognize that different systems have different needs, which means they need different operating systems. 

In Operating Systems with very small resources, they do not have a lot of functionality and are built to do the bare minimum.

For instance, **embedded systems** are built as small and cheap as possible. They maximize the resources that they have, and only have the resources that are absolutely necessary. Often in these systems, we know the workload in advance and do not need to worry about users. It's also arguable that these systems do not have an OS, if the code runs on 'bare metal'. However, if an OS exists, it might simply be a library that glues and links programs together. 

A **real-time system**, is a system which has a set workload, and a deadline to complete them. Often, there are major consequences on how we manage the resources, such as CPU time. A major consideration in real-time systems is what will happen if a deadline is missed.

If missing the deadline is bad, we call it a **soft real-time system**. For instance, a video codec needs to decode video and figure out to display within a set time (e.g., 30ms). If the codec misses the deadline, the video gets laggy.

If missing the deadline is catastrophic, we call it a **hard real-time system**. Examples of hard real-time systems include: Autopilot, Nuclear Power plant control, Health care devices. 