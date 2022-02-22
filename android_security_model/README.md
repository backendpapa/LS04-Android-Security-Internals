# Android's Security Model


## Introduction

This topic will help me understand Android architecture, Interprocess ommunication, Core component and Security models 


## Android's Architecture


### Linux Kernel
- Android is built on top of linux kernel
- The Linux kernel provides android the Harware, Networking, File system access and Process management.
- Android linux kernel is relatively different from the regular linux kernel with an extended feature known as **Androidisms**.
- Some Androidisms features include: Low memory killer, Wake locks, Anonymous share memory (ashmen), Alarms, Paranoid Networking, Bindings in IPC.

### Native UserSpace

- This spaces contains the **init** binary, which is the first process to get started.
- The **init** binary starts other processes.
- Native **daemons** and native **libraries** are found in this space.

### Dalvik VM

- large portion of Android is developed in Java, hence needs to be executed by a **JVM- Java Virtual Machine**
- Dalvix cannot run **.class** files, it can only run Dalvik executable codes **.dex**
- Dalvik is a register based VM, while Oracle VM is stack based

Note: **ART is the latest VM used by google**
- Dalvik uses fewer instructions compared to Oracle


### Java Runtime Libraries
- Java implementation requires runtime libraries mostly defined in the java.* or javax.*
- Java requires the **Java Native Interface** to make some native calls, these codes are linked with the java runtime libraries via JNI
- The runtime libraries are accessed by both the system service and the Applications


### System Services
- Implements most of the fundamental Android features such as:
1. Display and touch support
2. Telephony
3. Network connectivity
- Most system libraries are written in java,just a few in native.
- Each system service has an interface that allows other services or application to call them.
- Access is made possible by IPC provided by **Binders**,service discovery.


### Interprocess Communication

- Binder is an IPC mechanism.
- Each processes has an seperate address and a process cannot access another process's memory (process isolation)
- Process isolation prevents multiple processes from modifying the same memory address as it can be catastrophic.
- Other mechanisms like Shared memory,Message queue are not compatible with android.

#### Binders
- The binder IPC mechanism gives a process access to other process.
- All Android kernels have control over all processes, and therefore provide an interface for IPC. 
- The binder IPC device is found in **/dev/binder**, implemented by the kernel device driver

How is data passed between processes:
1. Binder driver manages part of the memory of each process involved.
2. These manages chunks are readonly to the process and can only be written via the kernel module.
3. Process A sends a message, the binder allocates some memory space in the receiving process's memory
4. Message is copied from the sender's allocated memory to the receiver's allocated memory.
5. a short message queue is sent to the receiving process telling it ,the memory address location to receive the message
6. The receipient can then access the message because its in its own address space
7. When a process is done with the message, it notifies the binder driver to mark the allocated memory free





