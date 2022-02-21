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

