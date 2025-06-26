# Unit I: Introduction to Operating Systems

## 0. Syllabus
Introduction to Operating Systems: Function, Evolution, Different Types, Desirable Characteristics and features of an O/S, Operating Systems Services: Types of Services, Different ways of providing these Services – Utility Programs, System Calls.

## 1. Introduction to Operating Systems

### What is an Operating System?
```
┌─────────────────────────────────────────────────────────────┐
│                 OPERATING SYSTEM                            │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │                    USER PROGRAMS                        │ │
│  │                                                         │ │
│  │  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐     │ │
│  │  │   Word      │  │   Browser   │  │   Games     │     │ │
│  │  │ Processor   │  │             │  │             │     │ │
│  │  └─────────────┘  └─────────────┘  └─────────────┘     │ │
│  └─────────────────────────────────────────────────────────┘ │
│                           │                                │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │                 OPERATING SYSTEM                        │ │
│  │                                                         │ │
│  │  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐     │ │
│  │  │   Process   │  │   Memory    │  │    File     │     │ │
│  │  │Management   │  │Management   │  │ Management  │     │ │
│  │  └─────────────┘  └─────────────┘  └─────────────┘     │ │
│  │                                                         │ │
│  │  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐     │ │
│  │  │   Device    │  │   Security  │  │   Network   │     │ │
│  │  │Management   │  │             │  │ Management  │     │ │
│  │  └─────────────┘  └─────────────┘  └─────────────┘     │ │
│  └─────────────────────────────────────────────────────────┘ │
│                           │                                │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │                    HARDWARE                             │ │
│  │                                                         │ │
│  │  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐     │ │
│  │  │     CPU     │  │    Memory   │  │    I/O      │     │ │
│  │  │             │  │             │  │  Devices    │     │ │
│  │  └─────────────┘  └─────────────┘  └─────────────┘     │ │
│  └─────────────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────────┘
```

**Definition**: An Operating System (OS) is system software that manages computer hardware, software resources, and provides common services for computer programs.

**Key Functions:**
- **Resource Manager**: Manages CPU, memory, I/O devices
- **Interface**: Provides user interface and program interface
- **Coordinator**: Coordinates between hardware and software
- **Protector**: Ensures security and protection

### Functions of Operating System
```
┌─────────────────────────────────────────────────────────────┐
│                 OS FUNCTIONS                                │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐         │
│  │   Process   │  │   Memory    │  │    File     │         │
│  │Management   │  │Management   │  │ Management  │         │
│  │             │  │             │  │             │         │
│  │ • Scheduling│  │ • Allocation│  │ • Creation  │         │
│  │ • Creation  │  │ • Protection│  │ • Deletion  │         │
│  │ • Termination│  │ • Swapping  │  │ • Access    │         │
│  └─────────────┘  └─────────────┘  └─────────────┘         │
│                                                             │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐         │
│  │   Device    │  │   Security  │  │   Network   │         │
│  │Management   │  │             │  │ Management  │         │
│  │             │  │             │  │             │         │
│  │ • Drivers   │  │ • Access    │  │ • Protocols │         │
│  │ • I/O       │  │   Control   │  │ • Routing   │         │
│  │ • Buffering │  │ • Encryption│  │ • Services  │         │
│  └─────────────┘  └─────────────┘  └─────────────┘         │
│                                                             │
│  ┌─────────────┐  ┌─────────────┐                          │
│  │   User      │  │   Error     │                          │
│  │ Interface   │  │  Handling   │                          │
│  │             │  │             │                          │
│  │ • GUI       │  │ • Detection │                          │
│  │ • CLI       │  │ • Recovery  │                          │
│  │ • API       │  │ • Prevention│                          │
│  └─────────────┘  └─────────────┘                          │
└─────────────────────────────────────────────────────────────┘
```

## 2. Evolution of Operating Systems

### 2.1 Batch Processing Systems (1940s-1950s)
```
┌─────────────────────────────────────────────────────────────┐
│                 BATCH PROCESSING                           │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  ┌─────────────┐    ┌─────────────┐    ┌─────────────┐     │
│  │   Job 1     │───▶│   Job 2     │───▶│   Job 3     │     │
│  │(Punched     │    │(Punched     │    │(Punched     │     │
│  │ Cards)      │    │ Cards)      │    │ Cards)      │     │
│  └─────────────┘    └─────────────┘    └─────────────┘     │
│         │                   │                   │           │
│         ▼                   ▼                   ▼           │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │                    BATCH QUEUE                          │ │
│  │                                                         │ │
│  │  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐     │ │
│  │  │   Input     │  │  Processing │  │   Output    │     │ │
│  │  │   Phase     │  │   Phase     │  │   Phase     │     │ │
│  │  └─────────────┘  └─────────────┘  └─────────────┘     │ │
│  └─────────────────────────────────────────────────────────┘ │
│                                                             │
│  ════════════════════════════════════════════════════════   │
│  Jobs processed sequentially without user interaction       │
└─────────────────────────────────────────────────────────────┘
```

**Characteristics:**
- Jobs collected in batches
- No user interaction during execution
- Sequential processing
- High CPU utilization

**Advantages:**
- Simple to implement
- Efficient CPU usage
- No user interaction overhead

**Disadvantages:**
- No interactivity
- Long turnaround time
- Poor resource utilization
- No multiprogramming

### 2.2 Multiprogramming Systems (1960s)
```
┌─────────────────────────────────────────────────────────────┐
│                 MULTIPROGRAMMING                           │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │                    MEMORY                               │ │
│  │                                                         │ │
│  │  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐     │ │
│  │  │   Job 1     │  │   Job 2     │  │   Job 3     │     │ │
│  │  │(CPU Bound)  │  │(I/O Bound)  │  │(CPU Bound)  │     │ │
│  │  │             │  │             │  │             │     │ │
│  │  └─────────────┘  └─────────────┘  └─────────────┘     │ │
│  └─────────────────────────────────────────────────────────┘ │
│                           │                                │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │                      CPU                                │ │
│  │                                                         │ │
│  │  ┌─────────────┐    ┌─────────────┐    ┌─────────────┐ │ │
│  │  │   Job 1     │───▶│   Job 2     │───▶│   Job 3     │ │ │
│  │  │(Executing)  │    │(Waiting for │    │(Executing)  │ │ │
│  │  │             │    │   I/O)      │    │             │ │ │
│  │  └─────────────┘    └─────────────┘    └─────────────┘ │ │
│  └─────────────────────────────────────────────────────────┘ │
│                                                             │
│  ════════════════════════════════════════════════════════   │
│  Multiple jobs in memory, CPU switches when I/O occurs     │
└─────────────────────────────────────────────────────────────┘
```

**Characteristics:**
- Multiple jobs in memory simultaneously
- CPU switches between jobs when I/O occurs
- Better resource utilization
- Job scheduling required

**Advantages:**
- Better CPU utilization
- Reduced idle time
- Improved throughput
- Better resource sharing

**Disadvantages:**
- Complex memory management
- Need for job scheduling
- Potential for deadlocks
- Security concerns

### 2.3 Time-Sharing Systems (1970s)
```
┌─────────────────────────────────────────────────────────────┐
│                 TIME-SHARING SYSTEMS                       │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐         │
│  │   User 1    │  │   User 2    │  │   User 3    │         │
│  │  Terminal   │  │  Terminal   │  │  Terminal   │         │
│  └─────────────┘  └─────────────┘  └─────────────┘         │
│         │                   │                   │           │
│         ▼                   ▼                   ▼           │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │                 TIME-SHARING OS                         │ │
│  │                                                         │ │
│  │  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐     │ │
│  │  │   Process   │  │   Process   │  │   Process   │     │ │
│  │  │    1        │  │    2        │  │    3        │     │ │
│  │  │             │  │             │  │             │     │ │
│  │  └─────────────┘  └─────────────┘  └─────────────┘     │ │
│  │         │                   │                   │       │ │
│  │         ▼                   ▼                   ▼       │ │
│  │  ┌─────────────────────────────────────────────────────┐ │ │
│  │  │                     CPU                             │ │ │
│  │  │  ┌─────┐  ┌─────┐  ┌─────┐  ┌─────┐  ┌─────┐      │ │ │
│  │  │  │ P1  │  │ P2  │  │ P3  │  │ P1  │  │ P2  │      │ │ │
│  │  │  └─────┘  └─────┘  └─────┘  └─────┘  └─────┘      │ │ │
│  │  └─────────────────────────────────────────────────────┘ │ │
│  └─────────────────────────────────────────────────────────┘ │
│                                                             │
│  ════════════════════════════════════════════════════════   │
│  CPU time shared among multiple users with quick switching  │
└─────────────────────────────────────────────────────────────┘
```

**Characteristics:**
- Multiple users share CPU time
- Quick context switching
- Interactive computing
- Real-time response

**Advantages:**
- Interactive computing
- Better user experience
- Resource sharing
- Cost-effective

**Disadvantages:**
- Complex scheduling
- Memory management overhead
- Security challenges
- Performance degradation with many users

### 2.4 Personal Computer Systems (1980s-1990s)
```
┌─────────────────────────────────────────────────────────────┐
│                 PERSONAL COMPUTER OS                       │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │                    SINGLE USER                          │ │
│  │                                                         │ │
│  │  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐     │ │
│  │  │   Desktop   │  │   Windows   │  │   Icons     │     │ │
│  │  │             │  │             │  │             │     │ │
│  │  └─────────────┘  └─────────────┘  └─────────────┘     │ │
│  └─────────────────────────────────────────────────────────┘ │
│                           │                                │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │                 GUI INTERFACE                           │ │
│  │                                                         │ │
│  │  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐     │ │
│  │  │   Mouse     │  │  Keyboard   │  │   Monitor   │     │ │
│  │  │   Events    │  │   Input     │  │   Display   │     │ │
│  │  └─────────────┘  └─────────────┘  └─────────────┘     │ │
│  └─────────────────────────────────────────────────────────┘ │
│                           │                                │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │                 HARDWARE                                │ │
│  │                                                         │ │
│  │  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐     │ │
│  │  │     CPU     │  │    Memory   │  │    I/O      │     │ │
│  │  │             │  │             │  │  Devices    │     │ │
│  │  └─────────────┘  └─────────────┘  └─────────────┘     │ │
│  └─────────────────────────────────────────────────────────┘ │
│                                                             │
│  ════════════════════════════════════════════════════════   │
│  Single user, GUI interface, personal computing             │
└─────────────────────────────────────────────────────────────┘
```

**Characteristics:**
- Single user system
- Graphical User Interface (GUI)
- Personal computing
- User-friendly

**Examples:**
- Windows 95/98/XP
- Mac OS
- Linux distributions

**Advantages:**
- User-friendly interface
- Personal control
- Rich applications
- Easy to use

**Disadvantages:**
- Limited resource sharing
- Security vulnerabilities
- Single point of failure
- Limited scalability

### 2.5 Modern Operating Systems (2000s-Present)
```
┌─────────────────────────────────────────────────────────────┐
│                 MODERN OPERATING SYSTEMS                   │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐         │
│  │   Desktop   │  │   Mobile    │  │   Embedded  │         │
│  │     OS      │  │     OS      │  │     OS      │         │
│  │             │  │             │  │             │         │
│  │ • Windows   │  │ • Android   │  │ • RTOS      │         │
│  │ • macOS     │  │ • iOS       │  │ • VxWorks   │         │
│  │ • Linux     │  │ • Windows   │  │ • QNX       │         │
│  └─────────────┘  └─────────────┘  └─────────────┘         │
│                                                             │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐         │
│  │   Cloud     │  │   Virtual   │  │   Real-time │         │
│  │     OS      │  │     OS      │  │     OS      │         │
│  │             │  │             │  │             │         │
│  │ • AWS       │  │ • VMware    │  │ • Hard RT   │         │
│  │ • Azure     │  │ • Hyper-V   │  │ • Soft RT   │         │
│  │ • GCP       │  │ • Docker    │  │ • Embedded  │         │
│  └─────────────┘  └─────────────┘  └─────────────┘         │
│                                                             │
│  ════════════════════════════════════════════════════════   │
│  Diverse platforms with specialized features                │
└─────────────────────────────────────────────────────────────┘
```

**Characteristics:**
- Multi-platform support
- Virtualization
- Cloud computing
- Real-time capabilities
- Security focus

## 3. Different Types of Operating Systems

### 3.1 Single-User Single-Task OS
```
┌─────────────────────────────────────────────────────────────┐
│              SINGLE-USER SINGLE-TASK                       │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │                    SINGLE USER                          │ │
│  │                                                         │ │
│  │  ┌─────────────┐                                        │ │
│  │  │   One Task  │                                        │ │
│  │  │  at a Time  │                                        │ │
│  │  │             │                                        │ │
│  │  │  ┌─────┐    │                                        │ │
│  │  │  │Task1│    │                                        │ │
│  │  │  └─────┘    │                                        │ │
│  │  │             │                                        │ │
│  │  │  ┌─────┐    │                                        │ │
│  │  │  │Task2│    │                                        │ │
│  │  │  └─────┘    │                                        │ │
│  │  │             │                                        │ │
│  │  │  ┌─────┐    │                                        │ │
│  │  │  │Task3│    │                                        │ │
│  │  │  └─────┘    │                                        │ │
│  │  └─────────────┘                                        │ │
│  └─────────────────────────────────────────────────────────┘ │
│                                                             │
│  Examples: MS-DOS, Palm OS                                 │
│  ════════════════════════════════════════════════════════   │
│  Only one user, one task at a time                         │
└─────────────────────────────────────────────────────────────┘
```

**Characteristics:**
- Only one user at a time
- Only one task at a time
- Simple resource management
- Limited functionality

**Examples:**
- MS-DOS
- Palm OS
- Early mobile OS

**Advantages:**
- Simple to implement
- Low resource requirements
- Predictable behavior
- Easy to understand

**Disadvantages:**
- Poor resource utilization
- No multitasking
- Limited functionality
- Poor user experience

### 3.2 Single-User Multi-Task OS
```
┌─────────────────────────────────────────────────────────────┐
│              SINGLE-USER MULTI-TASK                        │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │                    SINGLE USER                          │ │
│  │                                                         │ │
│  │  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐     │ │
│  │  │   Task 1    │  │   Task 2    │  │   Task 3    │     │ │
│  │  │(Word Proc)  │  │(Browser)    │  │(Music Player│     │ │
│  │  │             │  │             │  │             │     │ │
│  │  └─────────────┘  └─────────────┘  └─────────────┘     │ │
│  │         │                   │                   │       │ │
│  │         ▼                   ▼                   ▼       │ │
│  │  ┌─────────────────────────────────────────────────────┐ │ │
│  │  │                     CPU                             │ │ │
│  │  │  ┌─────┐  ┌─────┐  ┌─────┐  ┌─────┐  ┌─────┐      │ │ │
│  │  │  │ T1  │  │ T2  │  │ T3  │  │ T1  │  │ T2  │      │ │ │
│  │  │  └─────┘  └─────┘  └─────┘  └─────┘  └─────┘      │ │ │
│  │  └─────────────────────────────────────────────────────┘ │ │
│  └─────────────────────────────────────────────────────────┘ │
│                                                             │
│  Examples: Windows, macOS, Linux                           │
│  ════════════════════════════════════════════════════════   │
│  One user, multiple tasks simultaneously                   │
└─────────────────────────────────────────────────────────────┘
```

**Characteristics:**
- One user at a time
- Multiple tasks simultaneously
- Task scheduling required
- Memory management needed

**Examples:**
- Windows 10/11
- macOS
- Linux distributions

**Advantages:**
- Better resource utilization
- Improved user experience
- Multitasking capability
- Rich application support

**Disadvantages:**
- More complex
- Higher resource requirements
- Potential for conflicts
- Security challenges

### 3.3 Multi-User OS
```
┌─────────────────────────────────────────────────────────────┐
│                    MULTI-USER OS                           │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐         │
│  │   User 1    │  │   User 2    │  │   User 3    │         │
│  │  Terminal   │  │  Terminal   │  │  Terminal   │         │
│  └─────────────┘  └─────────────┘  └─────────────┘         │
│         │                   │                   │           │
│         ▼                   ▼                   ▼           │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │                 OPERATING SYSTEM                        │ │
│  │                                                         │ │
│  │  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐     │ │
│  │  │   Process   │  │   Process   │  │   Process   │     │ │
│  │  │   User 1    │  │   User 2    │  │   User 3    │     │ │
│  │  │             │  │             │  │             │     │ │
│  │  └─────────────┘  └─────────────┘  └─────────────┘     │ │
│  │         │                   │                   │       │ │
│  │         ▼                   ▼                   ▼       │ │
│  │  ┌─────────────────────────────────────────────────────┐ │ │
│  │  │                     CPU                             │ │ │
│  │  │  ┌─────┐  ┌─────┐  ┌─────┐  ┌─────┐  ┌─────┐      │ │ │
│  │  │  │ U1  │  │ U2  │  │ U3  │  │ U1  │  │ U2  │      │ │ │
│  │  │  └─────┘  └─────┘  └─────┘  └─────┘  └─────┘      │ │ │
│  │  └─────────────────────────────────────────────────────┘ │ │
│  └─────────────────────────────────────────────────────────┘ │
│                                                             │
│  Examples: Unix, Linux, Windows Server                     │
│  ════════════════════════════════════════════════════════   │
│  Multiple users share system resources                      │
└─────────────────────────────────────────────────────────────┘
```

**Characteristics:**
- Multiple users simultaneously
- Resource sharing
- User isolation
- Security and protection

**Examples:**
- Unix/Linux
- Windows Server
- Mainframe OS

**Advantages:**
- Resource sharing
- Cost-effective
- Centralized management
- Scalable

**Disadvantages:**
- Complex security
- Performance issues
- Resource contention
- Management overhead

### 3.4 Real-Time OS (RTOS)
```
┌─────────────────────────────────────────────────────────────┐
│                    REAL-TIME OS                            │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐         │
│  │   Hard RT   │  │   Soft RT   │  │  Firm RT    │         │
│  │             │  │             │  │             │         │
│  │ • Critical  │  │ • Important │  │ • Moderate  │         │
│  │   deadlines │  │   deadlines │  │   deadlines │         │
│  │ • No delay  │  │ • Some delay│  │ • Flexible  │         │
│  │   tolerance │  │   tolerance │  │   tolerance │         │
│  └─────────────┘  └─────────────┘  └─────────────┘         │
│                                                             │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐         │
│  │   Medical   │  │   Industrial│  │   Aerospace │         │
│  │   Devices   │  │   Control   │  │   Systems   │         │
│  │             │  │             │  │             │         │
│  │ • Pacemakers│  │ • Robotics  │  │ • Satellites│         │
│  │ • Monitors  │  │ • PLCs      │  │ • Missiles  │         │
│  │ • Scanners  │  │ • Sensors   │  │ • Aircraft  │         │
│  └─────────────┘  └─────────────┘  └─────────────┘         │
│                                                             │
│  ════════════════════════════════════════════════════════   │
│  Predictable timing for critical applications               │
└─────────────────────────────────────────────────────────────┘
```

**Characteristics:**
- Predictable timing
- Deadline constraints
- Priority-based scheduling
- Deterministic behavior

**Types:**
1. **Hard Real-Time**: Critical deadlines, no delay tolerance
2. **Soft Real-Time**: Important deadlines, some delay tolerance
3. **Firm Real-Time**: Moderate deadlines, flexible tolerance

**Examples:**
- VxWorks
- QNX
- FreeRTOS
- RTLinux

**Advantages:**
- Predictable performance
- Reliable timing
- Suitable for critical systems
- Deterministic behavior

**Disadvantages:**
- Limited functionality
- Complex development
- Resource constraints
- Expensive

### 3.5 Distributed OS
```
┌─────────────────────────────────────────────────────────────┐
│                  DISTRIBUTED OS                            │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐         │
│  │   Node 1    │  │   Node 2    │  │   Node 3    │         │
│  │             │  │             │  │             │         │
│  │ ┌─────────┐ │  │ ┌─────────┐ │  │ ┌─────────┐ │         │
│  │ │   OS    │ │  │ │   OS    │ │  │ │   OS    │ │         │
│  │ │         │ │  │ │         │ │  │ │         │ │         │
│  │ └─────────┘ │  │ └─────────┘ │  │ └─────────┘ │         │
│  └─────────────┘  └─────────────┘  └─────────────┘         │
│         │                   │                   │           │
│         └───────────────────┼───────────────────┘           │
│                             │                               │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │                 NETWORK LAYER                           │ │
│  │                                                         │ │
│  │  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐     │ │
│  │  │   Shared    │  │   Load      │  │   Fault     │     │ │
│  │  │  Resources  │  │ Balancing   │  │ Tolerance   │     │ │
│  │  └─────────────┘  └─────────────┘  └─────────────┘     │ │
│  └─────────────────────────────────────────────────────────┘ │
│                                                             │
│  Examples: Amoeba, Plan 9, Inferno                         │
│  ════════════════════════════════════════════════════════   │
│  Multiple nodes working as a single system                 │
└─────────────────────────────────────────────────────────────┘
```

**Characteristics:**
- Multiple nodes
- Shared resources
- Load balancing
- Fault tolerance

**Examples:**
- Amoeba
- Plan 9
- Inferno
- Distributed Linux

**Advantages:**
- Scalability
- Fault tolerance
- Resource sharing
- High availability

**Disadvantages:**
- Complex networking
- Synchronization issues
- Security challenges
- Performance overhead

## 4. Desirable Characteristics and Features

### 4.1 Essential Characteristics
```
┌─────────────────────────────────────────────────────────────┐
│              ESSENTIAL CHARACTERISTICS                     │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐         │
│  │  Efficiency │  │ Reliability │  │  Security   │         │
│  │             │  │             │  │             │         │
│  │ • Resource  │  │ • Stable    │  │ • Access    │         │
│  │   usage     │  │   operation │  │   control   │         │
│  │ • Fast      │  │ • Error     │  │ • Data      │         │
│  │   response  │  │   handling  │  │   protection│         │
│  └─────────────┘  └─────────────┘  └─────────────┘         │
│                                                             │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐         │
│  │ Scalability │  │ Usability   │  │ Portability │         │
│  │             │  │             │  │             │         │
│  │ • Handle    │  │ • User-     │  │ • Run on    │         │
│  │   growth    │  │   friendly  │  │   different │         │
│  │ • Adapt to  │  │ • Intuitive │  │   hardware  │         │
│  │   changes   │  │   interface │  │   platforms │         │
│  └─────────────┘  └─────────────┘  └─────────────┘         │
│                                                             │
│  ┌─────────────┐  ┌─────────────┐                          │
│  │Maintainability│ │ Extensibility│                          │
│  │             │  │             │                          │
│  │ • Easy to   │  │ • Easy to   │                          │
│  │   modify    │  │   extend    │                          │
│  │ • Debugging │  │ • Add new   │                          │
│  │   support   │  │   features  │                          │
│  └─────────────┘  └─────────────┘                          │
└─────────────────────────────────────────────────────────────┘
```

### 4.2 Key Features
```
┌─────────────────────────────────────────────────────────────┐
│                    KEY FEATURES                            │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │                 PROCESS MANAGEMENT                      │ │
│  │                                                         │ │
│  │  • Process creation and termination                     │ │
│  │  • Process scheduling and synchronization               │ │
│  │  • Inter-process communication                          │ │
│  │  • Deadlock handling                                    │ │
│  └─────────────────────────────────────────────────────────┘ │
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │                 MEMORY MANAGEMENT                       │ │
│  │                                                         │ │
│  │  • Memory allocation and deallocation                   │ │
│  │  • Virtual memory management                            │ │
│  │  • Memory protection and sharing                        │ │
│  │  • Paging and segmentation                              │ │
│  └─────────────────────────────────────────────────────────┘ │
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │                 FILE SYSTEM                             │ │
│  │                                                         │ │
│  │  • File creation, deletion, and manipulation            │ │
│  │  • Directory management                                 │ │
│  │  • File access control and security                     │ │
│  │  • File system organization                             │ │
│  └─────────────────────────────────────────────────────────┘ │
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │                 DEVICE MANAGEMENT                       │ │
│  │                                                         │ │
│  │  • Device drivers and I/O management                    │ │
│  │  • Device allocation and scheduling                     │ │
│  │  • Buffering and caching                                │ │
│  │  • Error handling and recovery                          │ │
│  └─────────────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────────┘
```

## 5. Operating System Services

### 5.1 Types of Services
```
┌─────────────────────────────────────────────────────────────┐
│                 OS SERVICES                                │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │                 USER SERVICES                           │ │
│  │                                                         │ │
│  │  • Program execution                                    │ │
│  │  • I/O operations                                       │ │
│  │  • File system manipulation                             │ │
│  │  • Communications                                       │ │
│  │  • Error detection and handling                         │ │
│  └─────────────────────────────────────────────────────────┘ │
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │               SYSTEM SERVICES                           │ │
│  │                                                         │ │
│  │  • Resource allocation                                  │ │
│  │  • Accounting                                           │ │
│  │  • Protection and security                              │ │
│  │  • System monitoring                                    │ │
│  │  • Performance optimization                             │ │
│  └─────────────────────────────────────────────────────────┘ │
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │              BACKGROUND SERVICES                        │ │
│  │                                                         │ │
│  │  • System initialization                                │ │
│  │  • Process scheduling                                   │ │
│  │  • Memory management                                    │ │
│  │  • Device management                                    │ │
│  │  • Network services                                     │ │
│  └─────────────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────────┘
```

### 5.2 User Services
```
┌─────────────────────────────────────────────────────────────┐
│                 USER SERVICES                              │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐         │
│  │   Program   │  │     I/O     │  │    File     │         │
│  │ Execution   │  │ Operations  │  │  System     │         │
│  │             │  │             │  │             │         │
│  │ • Load      │  │ • Read/Write│  │ • Create    │         │
│  │   programs  │  │ • Input/    │  │ • Delete    │         │
│  │ • Execute   │  │   Output    │  │ • Open/Close│         │
│  │ • Terminate │  │ • Device    │  │ • Read/Write│         │
│  └─────────────┘  └─────────────┘  └─────────────┘         │
│                                                             │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐         │
│  │Communications│  │   Error     │  │   User      │         │
│  │             │  │ Detection   │  │ Interface   │         │
│  │             │  │             │  │             │         │
│  │ • Inter-    │  │ • Hardware  │  │ • GUI       │         │
│  │   process   │  │   errors    │  │ • CLI       │         │
│  │ • Network   │  │ • Software  │  │ • API       │         │
│  │ • Remote    │  │   errors    │  │ • Help      │         │
│  └─────────────┘  └─────────────┘  └─────────────┘         │
│                                                             │
│  ════════════════════════════════════════════════════════   │
│  Services directly accessible to users                     │
└─────────────────────────────────────────────────────────────┘
```

### 5.3 System Services
```
┌─────────────────────────────────────────────────────────────┐
│               SYSTEM SERVICES                              │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐         │
│  │ Resource    │  │ Accounting  │  │ Protection  │         │
│  │ Allocation  │  │             │  │  & Security │         │
│  │             │  │ • Usage     │  │             │         │
│  │ • CPU       │  │   tracking  │  │ • Access    │         │
│  │ • Memory    │  │ • Billing   │  │   control   │         │
│  │ • Devices   │  │ • Resource  │  │ • Data      │         │
│  │ • Files     │  │   usage     │  │   protection│         │
│  └─────────────┘  └─────────────┘  └─────────────┘         │
│                                                             │
│  ┌─────────────┐  ┌─────────────┐                          │
│  │ System      │  │ Performance │                          │
│  │ Monitoring  │  │ Optimization│                          │
│  │             │  │             │                          │
│  │ • Logs      │  │ • Tuning    │                          │
│  │ • Alerts    │  │ • Load      │                          │
│  │ • Status    │  │   balancing │                          │
│  └─────────────┘  └─────────────┘                          │
│                                                             │
│  ════════════════════════════════════════════════════════   │
│  Services for system management and optimization            │
└─────────────────────────────────────────────────────────────┘
```

### 5.4 Background Services
```
┌─────────────────────────────────────────────────────────────┐
│              BACKGROUND SERVICES                            │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐         │
│  │ System      │  │ Process     │  │ Memory      │         │
│  │ Init/Boot   │  │ Scheduling  │  │ Management  │         │
│  │             │  │             │  │             │         │
│  │ • Startup   │  │ • CPU       │  │ • Allocation│         │
│  │ • Shutdown  │  │   allocation│  │ • Swapping  │         │
│  │ • Recovery  │  │ • Priorities│  │ • Protection│         │
│  └─────────────┘  └─────────────┘  └─────────────┘         │
│                                                             │
│  ┌─────────────┐  ┌─────────────┐                          │
│  │ Device      │  │ Network     │                          │
│  │ Management  │  │ Services    │                          │
│  │             │  │             │                          │
│  │ • Drivers   │  │ • Protocols │                          │
│  │ • I/O       │  │ • Routing   │                          │
│  │ • Buffering │  │ • Services  │                          │
│  └─────────────┘  └─────────────┘                          │
│                                                             │
│  ════════════════════════════════════════════════════════   │
│  Services running in the background for system operation    │
└─────────────────────────────────────────────────────────────┘
```

### 5.5 Different Ways of Providing Services

#### Utility Programs
- Standalone programs that perform specific tasks to support OS functions
- Examples: Disk cleanup, antivirus, backup tools, file compression, defragmentation
- Enhance usability and maintenance

#### System Calls
- Interface between user programs and OS services
- Allow programs to request services from the OS kernel
- Examples: open(), read(), write(), fork(), exec(), exit()
- Types: Process control, file management, device management, information maintenance, communication

---

## Quick Revision Points

### Key OS Types to Remember:
```
┌─────────────────────────────────────────────────────────────┐
│                    QUICK REFERENCE                          │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  1. Batch         → Sequential, no interaction              │
│  2. Multiprogram  → Multiple jobs, better utilization       │
│  3. Time-Sharing  → Interactive, multi-user                 │
│  4. Personal      → Single user, GUI                        │
│  5. Modern        → Multi-platform, virtualization          │
│  6. Real-Time     → Predictable, deadline-driven            │
│  7. Distributed   → Multiple nodes, resource sharing        │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

### Essential OS Characteristics:
- Efficiency, Reliability, Security, Scalability, Usability, Portability, Maintainability, Extensibility

### OS Services:
- User Services: Program execution, I/O, file management, communication, error handling
- System Services: Resource allocation, accounting, protection, monitoring, optimization
- Background Services: Init, scheduling, memory/device/network management
- Provided via: Utility Programs, System Calls