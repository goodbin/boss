# BOSS - Base objects for service solutions

Cross-platform component framework in C++11

**Boss gives you:**
- Ability of building loosely-coupled systems
- Minimal effort for creating new components
- Support for several operating systems
- Advantages of C++11
- Availability for open and proprietary software

Large projects written in C++ sometimes require system decomposition. A system under development can evolve from one executable
 to the complex multi-component large system. Furthermore, a system can be initially planned as a large software
 product. One can easily face a problem "What to use for system decomposition? How to organize components interaction?".
All these questions can be addressed by employing the component framework Boss.

Boss is aimed at providing tools for building a system of multiple components with a minimal effort.
 The Boss framework was started with an idea in mind "Minimalism everywhere where it is possible": minimal implementation,
 minimal amount of steps for creating and using components within the developing system.

At a stage when the system should get distributed Boss provides relatively smooth transition to a multi-process
 application, both within one computer or distributed in a cluster. The existent code should not be modified to archive
 such goals. All you need to do is to implement a Proxy/Stub module for each component. The spirit of the minimalism
 presents in the Proxy/Stub implementation as well. Finally, you modify the configuration of your system and you are done.

Boss does not provide specific implementations for auxiliary services and utilities. Instead, a developer should use ad
-hoc libraries. Boss is the way to efficiently glue your components into one software system.


## 1. Introduction

Software development always arise a question of system decomposition. A typical approach is to use shared libraries with exported functions. Another way to do it is to employ exported classes within a dll (it can make some troubles, especially after moving to another compiler) or export interfaces and load libraries manually. 

The component model of Boss lets user to abstract away from thinking of how to get a certain interface, how to load a dynamic library or how to set-up multi-process component interaction. The user defines components based on interfaces, registers them into the model, afterwards the component model takes care of providing simple mechanism for operating the components.

### 1.1 General information

The name Boss stands for Base Objects for Service Solutions. An alternative name is t-Boss. This model is aimed at development of cross-platform software with the weak coupling of its components.
 The supported operating systems are Linux, FreeBSD, Microsoft Windows.
The key features of Boss are minimalism and making use of C++11.

#### 1.1.1 What we can do with Boss?

The component model covers a wide range of problems. It can be used for developing both desktop applications and server software. For developing desktop applications Boss can be coupled with various frameworks, for example with Qt. Boss perfectly fits for producing plug-in based applications.


#### 1.1.2 Supported operating systems

Linux  - The framework was mostly tested under this OS.

FreeBSD - Supported. The framework was tested on FreeBSD 9.2 32bit

Microsoft Windows - Supported. Tested on Windows 7 32 bit.


#### 1.1.3 Supported compilers

gcc/g++  - Supported

MS VC++ 2013 - Supported with limitations: instead of the macro BOSS_DECLARE_IFACEID, used for defining a string-based identifier, one should use BOSS_DECLARE_IFACEID_HEX. This macro uses a number-based id, for example CRC32 of a string. It is also impossible to use the function Boss::MakeId for computing ids in compile-time.

clang - Boss must be tested and adjusted on demand.

#### 1.1.4 Integration with other libraries with Qt as an example

Under development

### 1.2. Components

Components are the implementations of user-defined interfaces (the notion of interface is explained further) with a given identifier. All the components are grouped into services (groups of components in different modules). There might be single-process or multi-process components (including remote interaction).

#### 1.2.1. In-process components (InProc)

In-process components are designed to be used within a single process. We can also call them "plugins". They are suited perfectly for developing desktop software with GUI as this sector of software rarely demands multi-process approach. Although, some additional elements of such software can go beyond the single-process mode. Such components are applicable for developing business-logic, for example server-side software. In-process components are optimal from viewpoint of access as they are handled directly by using a pointer to the interface. Typically, the inter-process marshaling introduces lags while calling each method.

#### 1.2.2 Inter-process components (OutOfProc)

Components designed for inter-process communication are developed the same way as in-process components. To employ inter-process features we develop a service-module for each interface with Proxy/Stub. There is a minimalistic set of macros introduced for defining Proxy/Stub. The components previously designed for the in-process usage are naturally extended for inter-process work. Inter-process components are supposed to be used within one computer but in different processes.

#### 1.2.3 Distributed system

A distributed system is a system of inter-process components with additional transport mechanism which extends the application to the cluster by using the network communication. Basically inter-process components and distributed components are the same components with a different transport layer. For example, one can use shared memory or another mechanisms or IPC within one machine and some network protocols for network distributed components. These two species of components are separated intentionally for  emphasizing various approaches of using Boss.
