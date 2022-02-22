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






