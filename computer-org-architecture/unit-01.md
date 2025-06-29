# Unit I: Basic Structure of Computer & Control Unit Organization

## 0. Syllabus
Basic Structure of Computer: Structure of Desktop Computers, CPU: General Register Organization-Memory Register, Instruction Register, Control Word, Stack Organization, Instruction Format, ALU, I/O System, bus, CPU and Memory Program Counter, Bus Structure, Register Transfer Language-Bus and Memory Transfer, addressing modes. Control Unit Organization: Basic Concept of Instruction, Instruction Types, Micro Instruction Formats, Fetch and Execution cycle, Hardwired control unit, Microprogrammed Control unit microprogram sequencer Control Memory, Sequencing and Execution of Micro Instruction.

## 1. Basic Structure of Computer

### Introduction to Computer Architecture
```
┌─────────────────────────────────────────────────────────────┐
│                COMPUTER ARCHITECTURE OVERVIEW              │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  Computer Architecture: Design of computer systems         │
│  involving both hardware and software                       │
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │                VON NEUMANN MODEL                        │ │
│  │                                                         │ │
│  │         ┌─────────────┐    ┌─────────────┐              │ │
│  │         │    INPUT    │    │   OUTPUT    │              │ │
│  │         │   DEVICES   │    │   DEVICES   │              │ │
│  │         └──────┬──────┘    └──────┬──────┘              │ │
│  │                │                  │                     │ │
│  │                ▼                  ▲                     │ │
│  │         ┌─────────────────────────────────┐              │ │
│  │         │      CENTRAL PROCESSING UNIT    │              │ │
│  │         │                                 │              │ │
│  │         │  ┌─────────────┐ ┌────────────┐ │              │ │
│  │         │  │    ALU      │ │  CONTROL   │ │              │ │
│  │         │  │             │ │    UNIT    │ │              │ │
│  │         │  └─────────────┘ └────────────┘ │              │ │
│  │         └─────────────┬───────────────────┘              │ │
│  │                       │                                  │ │
│  │                       ▼                                  │ │
│  │         ┌─────────────────────────────────┐              │ │
│  │         │           MEMORY               │              │ │
│  │         │     (Instructions + Data)      │              │ │
│  │         └─────────────────────────────────┘              │ │
│  └─────────────────────────────────────────────────────────┘ │
│                                                             │
│  Key Principles:                                           │
│  • Stored Program Concept                                  │
│  • Data and instructions in same memory                    │
│  • Sequential execution of instructions                    │
│  • Binary representation of information                    │
└─────────────────────────────────────────────────────────────┘
```

### Structure of Desktop Computers
```
┌─────────────────────────────────────────────────────────────┐
│                DESKTOP COMPUTER STRUCTURE                  │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │                  MOTHERBOARD                            │ │
│  │                                                         │ │
│  │  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐      │ │
│  │  │     CPU     │  │    RAM      │  │    ROM      │      │ │
│  │  │             │  │             │  │             │      │ │
│  │  │ ┌─────────┐ │  │ ┌─────────┐ │  │ ┌─────────┐ │      │ │
│  │  │ │   ALU   │ │  │ │  DRAM   │ │  │ │  BIOS   │ │      │ │
│  │  │ └─────────┘ │  │ └─────────┘ │  │ └─────────┘ │      │ │
│  │  │ ┌─────────┐ │  │ ┌─────────┐ │  │ ┌─────────┐ │      │ │
│  │  │ │CONTROL  │ │  │ │  SRAM   │ │  │ │ UEFI    │ │      │ │
│  │  │ │  UNIT   │ │  │ └─────────┘ │  │ └─────────┘ │      │ │
│  │  │ └─────────┘ │  └─────────────┘  └─────────────┘      │ │
│  │  │ ┌─────────┐ │                                        │ │
│  │  │ │REGISTER │ │  ┌─────────────┐  ┌─────────────┐      │ │
│  │  │ │  FILE   │ │  │   CACHE     │  │    GPU      │      │ │
│  │  │ └─────────┘ │  │             │  │             │      │ │
│  │  └─────────────┘  │ ┌─────────┐ │  │ ┌─────────┐ │      │ │
│  │                   │ │   L1    │ │  │ │ SHADER  │ │      │ │
│  │  ┌─────────────┐  │ └─────────┘ │  │ │  CORES  │ │      │ │
│  │  │  CHIPSET    │  │ ┌─────────┐ │  │ └─────────┘ │      │ │
│  │  │             │  │ │   L2    │ │  │ ┌─────────┐ │      │ │
│  │  │ ┌─────────┐ │  │ └─────────┘ │  │ │ VRAM    │ │      │ │
│  │  │ │NORTHBRIDG│ │  │ ┌─────────┐ │  │ └─────────┘ │      │ │
│  │  │ └─────────┘ │  │ │   L3    │ │  └─────────────┘      │ │
│  │  │ ┌─────────┐ │  │ └─────────┘ │                       │ │
│  │  │ │SOUTHBRIDG│ │  └─────────────┘                       │ │
│  │  │ └─────────┘ │                                        │ │
│  │  └─────────────┘                                        │ │
│  │                                                         │ │
│  │  ┌─────────────────────────────────────────────────────┐ │ │
│  │  │                BUS SYSTEM                           │ │ │
│  │  │                                                     │ │ │
│  │  │  ┌─────────┐ ┌─────────┐ ┌─────────┐ ┌─────────┐   │ │ │
│  │  │  │   CPU   │ │  Memory │ │   I/O   │ │ System  │   │ │ │
│  │  │  │   Bus   │ │   Bus   │ │   Bus   │ │   Bus   │   │ │ │
│  │  │  └─────────┘ └─────────┘ └─────────┘ └─────────┘   │ │ │
│  │  └─────────────────────────────────────────────────────┘ │ │
│  └─────────────────────────────────────────────────────────┘ │
│                                                             │
│  External Components:                                      │
│  • Storage: HDD, SSD, Optical Drives                      │
│  • Input: Keyboard, Mouse, Microphone                     │
│  • Output: Monitor, Speakers, Printer                     │
│  • Network: Ethernet, Wi-Fi, Bluetooth                    │
└─────────────────────────────────────────────────────────────┘
```

## 2. Central Processing Unit (CPU)

### CPU Architecture Overview
```
┌─────────────────────────────────────────────────────────────┐
│                    CPU ARCHITECTURE                        │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │                    CPU COMPONENTS                       │ │
│  │                                                         │ │
│  │  ┌─────────────────┐      ┌─────────────────┐          │ │
│  │  │  CONTROL UNIT   │      │ ARITHMETIC LOGIC│          │ │
│  │  │                 │      │     UNIT        │          │ │
│  │  │ ┌─────────────┐ │      │                 │          │ │
│  │  │ │ INSTRUCTION │ │      │ ┌─────────────┐ │          │ │
│  │  │ │   DECODER   │ │      │ │ ARITHMETIC  │ │          │ │
│  │  │ └─────────────┘ │      │ │   CIRCUITS  │ │          │ │
│  │  │ ┌─────────────┐ │      │ └─────────────┘ │          │ │
│  │  │ │  CONTROL    │ │      │ ┌─────────────┐ │          │ │
│  │  │ │  SIGNALS    │ │      │ │   LOGIC     │ │          │ │
│  │  │ │ GENERATOR   │ │      │ │  CIRCUITS   │ │          │ │
│  │  │ └─────────────┘ │      │ └─────────────┘ │          │ │
│  │  │ ┌─────────────┐ │      │ ┌─────────────┐ │          │ │
│  │  │ │   TIMING    │ │      │ │   STATUS    │ │          │ │
│  │  │ │   CONTROL   │ │      │ │   FLAGS     │ │          │ │
│  │  │ └─────────────┘ │      │ └─────────────┘ │          │ │
│  │  └─────────────────┘      └─────────────────┘          │ │
│  │                                                         │ │
│  │  ┌─────────────────────────────────────────────────────┐ │ │
│  │  │                REGISTER FILE                        │ │ │
│  │  │                                                     │ │ │
│  │  │ ┌─────────┐ ┌─────────┐ ┌─────────┐ ┌─────────┐    │ │ │
│  │  │ │  R0-R7  │ │ R8-R15  │ │R16-R23  │ │R24-R31  │    │ │ │
│  │  │ │ General │ │ General │ │ General │ │ General │    │ │ │
│  │  │ │Purpose  │ │Purpose  │ │Purpose  │ │Purpose  │    │ │ │
│  │  │ └─────────┘ └─────────┘ └─────────┘ └─────────┘    │ │ │
│  │  │                                                     │ │ │
│  │  │ ┌─────────┐ ┌─────────┐ ┌─────────┐ ┌─────────┐    │ │ │
│  │  │ │   PC    │ │   IR    │ │   MAR   │ │   MDR   │    │ │ │
│  │  │ │Program  │ │Instruction│ │Memory  │ │ Memory  │    │ │ │
│  │  │ │Counter  │ │Register │ │Address  │ │  Data   │    │ │ │
│  │  │ └─────────┘ └─────────┘ └─────────┘ └─────────┘    │ │ │
│  │  │                                                     │ │ │
│  │  │ ┌─────────┐ ┌─────────┐ ┌─────────┐ ┌─────────┐    │ │ │
│  │  │ │   SP    │ │   PSW   │ │   AC    │ │   DR    │    │ │ │
│  │  │ │ Stack   │ │Processor│ │Accumulator│ │  Data   │    │ │ │
│  │  │ │Pointer  │ │Status   │ │         │ │Register │    │ │ │
│  │  │ └─────────┘ └─────────┘ └─────────┘ └─────────┘    │ │ │
│  │  └─────────────────────────────────────────────────────┘ │ │
│  └─────────────────────────────────────────────────────────┘ │
│                                                             │
│  Key Functions:                                            │
│  • Fetch instructions from memory                          │
│  • Decode instructions                                     │
│  • Execute operations                                      │
│  • Store results                                           │
│  • Control system operation                                │
└─────────────────────────────────────────────────────────────┘
```

### General Register Organization
```
┌─────────────────────────────────────────────────────────────┐
│               GENERAL REGISTER ORGANIZATION                │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  32-Bit Register Architecture Example:                     │
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │                  REGISTER FILE                          │ │
│  │                                                         │ │
│  │  R0:  [00000000000000000000000000000000] - General     │ │
│  │  R1:  [00000000000000000000000000000000] - General     │ │
│  │  R2:  [00000000000000000000000000000000] - General     │ │
│  │  R3:  [00000000000000000000000000000000] - General     │ │
│  │  R4:  [00000000000000000000000000000000] - General     │ │
│  │  R5:  [00000000000000000000000000000000] - General     │ │
│  │  R6:  [00000000000000000000000000000000] - General     │ │
│  │  R7:  [00000000000000000000000000000000] - General     │ │
│  │                                                         │ │
│  │  SP:  [00000000000000000000000000000000] - Stack Ptr   │ │
│  │  LR:  [00000000000000000000000000000000] - Link Reg    │ │
│  │  PC:  [00000000000000000000000000000000] - Prog Cntr   │ │
│  │  PSR: [00000000000000000000000000000000] - Status Reg  │ │
│  └─────────────────────────────────────────────────────────┘ │
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │                REGISTER SELECTION                       │ │
│  │                                                         │ │
│  │     Source A    Source B    Destination                │ │
│  │  ┌─────────┐  ┌─────────┐  ┌─────────┐                 │ │
│  │  │  3-bit  │  │  3-bit  │  │  3-bit  │                 │ │
│  │  │ Decoder │  │ Decoder │  │ Decoder │                 │ │
│  │  └─────────┘  └─────────┘  └─────────┘                 │ │
│  │       │           │           │                        │ │
│  │       ▼           ▼           ▼                        │ │
│  │  ┌─────────┐  ┌─────────┐  ┌─────────┐                 │ │
│  │  │   MUX   │  │   MUX   │  │  DEMUX  │                 │ │
│  │  │  8:1    │  │  8:1    │  │  1:8    │                 │ │
│  │  └─────────┘  └─────────┘  └─────────┘                 │ │
│  │       │           │           │                        │ │
│  │       ▼           ▼           ▼                        │ │
│  │  ┌─────────────────────────────────┐                   │ │
│  │  │              ALU                │                   │ │
│  │  │                                 │                   │ │
│  │  │  A ── Operation ── B = Result   │                   │ │
│  │  └─────────────────────────────────┘                   │ │
│  └─────────────────────────────────────────────────────────┘ │
│                                                             │
│  Advantages of General Register Organization:              │
│  • Fast access to frequently used data                     │
│  • Reduces memory access                                   │
│  • Flexible instruction formats                            │
│  • Efficient compiler code generation                      │
└─────────────────────────────────────────────────────────────┘
```

### Memory Register (MAR & MDR)
```
┌─────────────────────────────────────────────────────────────┐
│                   MEMORY REGISTERS                         │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │         MEMORY ADDRESS REGISTER (MAR)                  │ │
│  │                                                         │ │
│  │  Purpose: Holds the address of memory location         │ │
│  │           to be accessed                                │ │
│  │                                                         │ │
│  │  MAR: [00110101010011101010101011110000]               │ │
│  │        │                               │                │ │
│  │        └─── 32-bit Memory Address ─────┘                │ │
│  │                                                         │ │
│  │  Address Range: 0x00000000 to 0xFFFFFFFF               │ │
│  │  (4 GB addressable memory space)                       │ │
│  └─────────────────────────────────────────────────────────┘ │
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │          MEMORY DATA REGISTER (MDR)                    │ │
│  │                                                         │ │
│  │  Purpose: Holds data being transferred to/from memory  │ │
│  │                                                         │ │
│  │  MDR: [11010010100111010101010110100011]               │ │
│  │        │                               │                │ │
│  │        └─── 32-bit Data Word ──────────┘                │ │
│  │                                                         │ │
│  │  Can hold: Instructions, Data, Addresses               │ │
│  └─────────────────────────────────────────────────────────┘ │
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │               MEMORY ACCESS OPERATION                   │ │
│  │                                                         │ │
│  │  Read Operation:                                        │ │
│  │  1. CPU loads address into MAR                         │ │
│  │  2. Memory control sends READ signal                    │ │
│  │  3. Memory places data on data bus                      │ │
│  │  4. Data is loaded into MDR                             │ │
│  │                                                         │ │
│  │  Write Operation:                                       │ │
│  │  1. CPU loads address into MAR                         │ │
│  │  2. CPU loads data into MDR                             │ │
│  │  3. Memory control sends WRITE signal                   │ │
│  │  4. Data from MDR is written to memory                  │ │
│  │                                                         │ │
│  │     CPU                    Memory                       │ │
│  │  ┌─────────┐             ┌─────────┐                    │ │
│  │  │   MAR   │───Address───│ Address │                    │ │
│  │  │         │    Bus      │ Decoder │                    │ │
│  │  └─────────┘             └─────────┘                    │ │
│  │  ┌─────────┐                  │                        │ │
│  │  │   MDR   │───Data Bus───────┼──────Storage Array      │ │
│  │  │         │                  │                        │ │
│  │  └─────────┘             ┌─────────┐                    │ │
│  │                          │ Control │                    │ │
│  │  Control ────────────────│   Unit  │                    │ │
│  │   Signals                └─────────┘                    │ │
│  └─────────────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────────┘
```

### Instruction Register (IR)
```
┌─────────────────────────────────────────────────────────────┐
│                 INSTRUCTION REGISTER (IR)                  │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  Purpose: Holds the current instruction being executed     │
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │                32-BIT INSTRUCTION FORMAT               │ │
│  │                                                         │ │
│  │  IR: [10110100│01001│01010│00000│00000000000│1]         │ │
│  │       │       │     │     │     │          │            │ │
│  │       │       │     │     │     │          │            │ │
│  │      Op       │     │     │     │          │            │ │
│  │     Code      │    Rs    Rt   Rd  Shamt   Funct       │ │
│  │    (6 bits)   │(5 bits)(5 bits)(5 bits)(5 bits)(6 bits)│ │
│  └─────────────────────────────────────────────────────────┘ │
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │                 INSTRUCTION FIELDS                      │ │
│  │                                                         │ │
│  │  Op Code (Operation Code):                             │ │
│  │  • Specifies the operation to be performed             │ │
│  │  • 6 bits = 64 possible operations                     │ │
│  │  • Examples: ADD, SUB, LOAD, STORE, BRANCH             │ │
│  │                                                         │ │
│  │  Rs (Source Register 1):                               │ │
│  │  • First source operand register                       │ │
│  │  • 5 bits = 32 possible registers                      │ │
│  │                                                         │ │
│  │  Rt (Source Register 2):                               │ │
│  │  • Second source operand register                      │ │
│  │  • Also used as destination for immediate operations   │ │
│  │                                                         │ │
│  │  Rd (Destination Register):                            │ │
│  │  • Register where result is stored                     │ │
│  │  • Used in R-type instructions                         │ │
│  │                                                         │ │
│  │  Shamt (Shift Amount):                                 │ │
│  │  • Used in shift operations                            │ │
│  │  • 5 bits = 0 to 31 shift positions                    │ │
│  │                                                         │ │
│  │  Funct (Function):                                     │ │
│  │  • Additional operation specification                   │ │
│  │  • Used with R-type instructions                       │ │
│  └─────────────────────────────────────────────────────────┘ │
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │                INSTRUCTION TYPES                        │ │
│  │                                                         │ │
│  │  R-Type (Register): Register-to-register operations    │ │
│  │  [Op Code│Rs│Rt│Rd│Shamt│Funct]                        │ │
│  │                                                         │ │
│  │  I-Type (Immediate): Operations with immediate values  │ │
│  │  [Op Code│Rs│Rt│    Immediate (16 bits)    ]           │ │
│  │                                                         │ │
│  │  J-Type (Jump): Jump and procedure call instructions   │ │
│  │  [Op Code│      Jump Address (26 bits)      ]          │ │
│  └─────────────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────────┘
```

### Control Word
```
┌─────────────────────────────────────────────────────────────┐
│                     CONTROL WORD                           │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  Control Word: A bit pattern that specifies the micro-     │
│  operations to be performed during an instruction cycle    │
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │               32-BIT CONTROL WORD                       │ │
│  │                                                         │ │
│  │  [SELA│SELB│SELD│FI│WE│RD│WR│MD│BS│PS│MW│...]           │ │
│  │   3   │ 3  │ 3  │2 │1 │1 │1 │1 │1 │1 │1 │            │ │
│  │  bits │bits│bits│  │  │  │  │  │  │  │  │             │ │
│  └─────────────────────────────────────────────────────────┘ │
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │               CONTROL FIELDS                            │ │
│  │                                                         │ │
│  │  SELA (3 bits): Select register A (source 1)           │ │
│  │  • 000: R0, 001: R1, 010: R2, ... 111: R7            │ │
│  │                                                         │ │
│  │  SELB (3 bits): Select register B (source 2)           │ │
│  │  • Same encoding as SELA                               │ │
│  │                                                         │ │
│  │  SELD (3 bits): Select destination register            │ │
│  │  • Where result will be stored                         │ │
│  │                                                         │ │
│  │  FI (2 bits): Function select for ALU                  │ │
│  │  • 00: ADD, 01: SUB, 10: AND, 11: OR                  │ │
│  │                                                         │ │
│  │  WE (1 bit): Write enable                              │ │
│  │  • 1: Enable write to destination register             │ │
│  │  • 0: Disable write (for comparison operations)        │ │
│  │                                                         │ │
│  │  RD (1 bit): Memory read enable                        │ │
│  │  WR (1 bit): Memory write enable                       │ │
│  │  MD (1 bit): Memory/ALU data select                    │ │
│  │  BS (1 bit): Bus select                                │ │
│  │  PS (1 bit): Program counter select                    │ │
│  │  MW (1 bit): Memory word select                        │ │
│  └─────────────────────────────────────────────────────────┘ │
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │               CONTROL WORD EXAMPLE                      │ │
│  │                                                         │ │
│  │  Instruction: ADD R1, R2, R3                           │ │
│  │  Operation: R3 ← R1 + R2                               │ │
│  │                                                         │ │
│  │  Control Word: [001│010│011│00│1│0│0│0│0│0│0│...]      │ │
│  │                 │   │   │   │  │ │ │ │ │ │ │            │ │
│  │               R1  R2  R3 ADD │ │ │ │ │ │ │             │ │
│  │              src src dest    │ │ │ │ │ │ │             │ │
│  │                           write│ │ │ │ │ │             │ │
│  │                           enable│ │ │ │ │              │ │
│  │                              no read/write             │ │
│  └─────────────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────────┘
```

## 3. Stack Organization

### Stack Concept and Structure
```
┌─────────────────────────────────────────────────────────────┐
│                    STACK ORGANIZATION                      │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  Stack: A Last-In-First-Out (LIFO) data structure         │
│  used for temporary data storage and procedure calls       │
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │                  STACK MEMORY                           │ │
│  │                                                         │ │
│  │  Higher  ┌─────────────────┐ ← Stack Base (SB)          │ │
│  │ Address  │                 │                            │ │
│  │          │                 │                            │ │
│  │          │     UNUSED      │                            │ │
│  │          │     SPACE       │                            │ │
│  │          │                 │                            │ │
│  │          ├─────────────────┤                            │ │
│  │          │     Data 3      │ ← Stack Top                │ │
│  │          ├─────────────────┤                            │ │
│  │          │     Data 2      │                            │ │
│  │          ├─────────────────┤                            │ │
│  │          │     Data 1      │                            │ │
│  │          ├─────────────────┤                            │ │
│  │   Lower  │     Data 0      │ ← Stack Pointer (SP)       │ │
│  │ Address  └─────────────────┘                            │ │
│  │                                                         │ │
│  │  SP Register: [00000000000000000000101100001000]       │ │
│  │              Points to last pushed item                 │ │
│  └─────────────────────────────────────────────────────────┘ │
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │                STACK OPERATIONS                         │ │
│  │                                                         │ │
│  │  PUSH Operation (Add item to stack):                   │ │
│  │  1. SP ← SP - 1    (Decrement stack pointer)           │ │
│  │  2. M[SP] ← Data   (Store data at SP location)         │ │
│  │                                                         │ │
│  │  POP Operation (Remove item from stack):               │ │
│  │  1. Data ← M[SP]   (Read data from SP location)        │ │
│  │  2. SP ← SP + 1    (Increment stack pointer)           │ │
│  │                                                         │ │
│  │  Stack Full Condition: SP = Stack Base - Stack Size    │ │
│  │  Stack Empty Condition: SP = Stack Base                │ │
│  └─────────────────────────────────────────────────────────┘ │
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │                 PUSH EXAMPLE                            │ │
│  │                                                         │ │
│  │  Initial State:    After PUSH 25:   After PUSH 30:     │ │
│  │                                                         │ │
│  │  SP→ [Empty]       SP→ [  30  ]      SP→ [  30  ]      │ │
│  │      [Empty]           [  25  ]          [  25  ]      │ │
│  │      [Empty]           [Empty]           [Empty]       │ │
│  │                                                         │ │
│  │  SP = 1000         SP = 999         SP = 998           │ │
│  └─────────────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────────┘
```

### Stack Applications
```
┌─────────────────────────────────────────────────────────────┐
│                   STACK APPLICATIONS                       │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │             SUBROUTINE CALL MECHANISM                   │ │
│  │                                                         │ │
│  │  1. CALL Instruction:                                  │ │
│  │     • Push return address onto stack                   │ │
│  │     • Jump to subroutine address                       │ │
│  │                                                         │ │
│  │  2. Subroutine Execution:                              │ │
│  │     • Push local variables                             │ │
│  │     • Execute subroutine code                          │ │
│  │                                                         │ │
│  │  3. RETURN Instruction:                                │ │
│  │     • Pop local variables                              │ │
│  │     • Pop return address                               │ │
│  │     • Jump to return address                           │ │
│  │                                                         │ │
│  │  Stack Frame Structure:                                │ │
│  │  ┌─────────────────┐                                   │ │
│  │  │ Return Address  │ ← Saved during CALL               │ │
│  │  ├─────────────────┤                                   │ │
│  │  │ Saved Registers │ ← Previous register values        │ │
│  │  ├─────────────────┤                                   │ │
│  │  │ Local Variables │ ← Subroutine local data           │ │
│  │  ├─────────────────┤                                   │ │
│  │  │   Parameters    │ ← Input parameters                │ │
│  │  └─────────────────┘                                   │ │
│  └─────────────────────────────────────────────────────────┘ │
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │              INTERRUPT HANDLING                         │ │
│  │                                                         │ │
│  │  When interrupt occurs:                                │ │
│  │  1. Push Program Counter (PC)                          │ │
│  │  2. Push Processor Status Word (PSW)                   │ │
│  │  3. Push working registers                             │ │
│  │  4. Load interrupt service routine address             │ │
│  │                                                         │ │
│  │  When returning from interrupt:                        │ │
│  │  1. Pop working registers                              │ │
│  │  2. Pop PSW                                            │ │
│  │  3. Pop PC                                             │ │
│  │  4. Resume normal execution                            │ │
│  └─────────────────────────────────────────────────────────┘ │
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │              EXPRESSION EVALUATION                      │ │
│  │                                                         │ │
│  │  Infix to Postfix conversion and evaluation            │ │
│  │                                                         │ │
│  │  Example: (A + B) * C                                  │ │
│  │  Postfix: A B + C *                                    │ │
│  │                                                         │ │
│  │  Evaluation Stack:                                     │ │
│  │  1. Push A                                             │ │
│  │  2. Push B                                             │ │
│  │  3. Pop B, Pop A, Push (A+B)                           │ │
│  │  4. Push C                                             │ │
│  │  5. Pop C, Pop (A+B), Push ((A+B)*C)                   │ │
│  └─────────────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────────┘
```

## 4. Instruction Format & ALU

### Instruction Format Types
```
┌─────────────────────────────────────────────────────────────┐
│                  INSTRUCTION FORMATS                       │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │               R-TYPE INSTRUCTIONS                       │ │
│  │                                                         │ │
│  │  Used for: Register-to-register operations             │ │
│  │                                                         │ │
│  │  31    26 25   21 20   16 15   11 10    6 5      0      │ │
│  │  ┌──────┬──────┬──────┬──────┬──────┬──────────┐        │ │
│  │  │  Op  │  Rs  │  Rt  │  Rd  │Shamt │   Funct  │        │ │
│  │  │ Code │      │      │      │      │          │        │ │
│  │  └──────┴──────┴──────┴──────┴──────┴──────────┘        │ │
│  │    6     5      5      5      5        6 bits          │ │
│  │                                                         │ │
│  │  Examples:                                              │ │
│  │  • ADD R1, R2, R3    (R3 = R1 + R2)                   │ │
│  │  • SUB R4, R5, R6    (R6 = R4 - R5)                   │ │
│  │  • AND R7, R8, R9    (R9 = R7 & R8)                   │ │
│  │  • SLL R1, R2, 4     (R2 = R1 << 4)                   │ │
│  │  └─────────────────────────────────────────────────────────┘ │
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │               I-TYPE INSTRUCTIONS                       │ │
│  │                                                         │ │
│  │  Used for: Immediate operations, Load/Store, Branches  │ │
│  │                                                         │ │
│  │  31    26 25   21 20   16 15                    0       │ │
│  │  ┌──────┬──────┬──────┬─────────────────────────┐       │ │
│  │  │  Op  │  Rs  │  Rt  │       Immediate         │       │ │
│  │  │ Code │      │      │                         │       │ │
│  │  └──────┴──────┴──────┴─────────────────────────┘       │ │
│  │    6     5      5              16 bits                 │ │
│  │                                                         │ │
│  │  Examples:                                              │ │
│  │  • ADDI R1, R2, #100  (R2 = R1 + 100)                 │ │
│  │  • LW R3, 8(R4)       (R3 = Memory[R4 + 8])           │ │
│  │  • SW R5, 12(R6)      (Memory[R6 + 12] = R5)          │ │
│  │  • BEQ R7, R8, Label  (if R7=R8 goto Label)           │ │
│  │  └─────────────────────────────────────────────────────────┘ │
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │               J-TYPE INSTRUCTIONS                       │ │
│  │                                                         │ │
│  │  Used for: Jump operations, Procedure calls            │ │
│  │                                                         │ │
│  │  31    26 25                                    0       │ │
│  │  ┌──────┬───────────────────────────────────────┐       │ │
│  │  │  Op  │            Jump Address              │       │ │
│  │  │ Code │                                       │       │ │
│  │  └──────┴───────────────────────────────────────┘       │ │
│  │    6                    26 bits                        │ │
│  │                                                         │ │
│  │  Examples:                                              │ │
│  │  • J Address         (PC = Address)                    │ │
│  │  • JAL Procedure     (R31 = PC+4, PC = Procedure)      │ │
│  │  └─────────────────────────────────────────────────────────┘ │
│  └─────────────────────────────────────────────────────────────┘ │
```

### Arithmetic Logic Unit (ALU)
```
┌─────────────────────────────────────────────────────────────┐
│                ARITHMETIC LOGIC UNIT (ALU)                 │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  ALU: The computational heart of the CPU that performs     │
│  arithmetic and logical operations                          │
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │                   ALU STRUCTURE                         │ │
│  │                                                         │ │
│  │              A (32 bits)    B (32 bits)                │ │
│  │                   │            │                       │ │
│  │                   ▼            ▼                       │ │
│  │            ┌────────────────────────────┐               │ │
│  │            │                            │               │ │
│  │  Control   │        ALU CORE            │               │ │
│  │  ────────→ │                            │               │ │
│  │  (4 bits)  │  ┌──────────┐ ┌──────────┐ │               │ │
│  │            │  │ARITHMETIC│ │  LOGIC   │ │               │ │
│  │            │  │   UNIT   │ │   UNIT   │ │               │ │
│  │            │  └──────────┘ └──────────┘ │               │ │
│  │            │                            │               │ │
│  │            │  ┌──────────┐ ┌──────────┐ │               │ │
│  │            │  │  SHIFT   │ │COMPARATOR│ │               │ │
│  │            │  │   UNIT   │ │          │ │               │ │
│  │            │  └──────────┘ └──────────┘ │               │ │
│  │            └────────────────────────────┘               │ │
│  │                           │                             │ │
│  │                           ▼                             │ │
│  │                  Result (32 bits)                      │ │
│  │                           │                             │ │
│  │                           ▼                             │ │
│  │                 ┌──────────────────┐                    │ │
│  │                 │   STATUS FLAGS   │                    │ │
│  │                 │                  │                    │ │
│  │                 │ Z N C V .... ... │                    │ │
│  │                 └──────────────────┘                    │ │
│  └─────────────────────────────────────────────────────────┘ │
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │                 ALU OPERATIONS                          │ │
│  │                                                         │ │
│  │  Control │ Operation │ Function                         │ │
│  │  ────────┼───────────┼─────────────────────────────     │ │
│  │   0000   │    ADD    │ A + B                           │ │
│  │   0001   │    SUB    │ A - B                           │ │
│  │   0010   │    AND    │ A & B                           │ │
│  │   0011   │    OR     │ A | B                           │ │
│  │   0100   │    XOR    │ A ⊕ B                           │ │
│  │   0101   │    NOT    │ ~A                              │ │
│  │   0110   │    SLL    │ A << B (Shift Left Logical)     │ │
│  │   0111   │    SRL    │ A >> B (Shift Right Logical)    │ │
│  │   1000   │    SRA    │ A >> B (Shift Right Arith)      │ │
│  │   1001   │    CMP    │ Compare A and B                 │ │
│  │   1010   │    MUL    │ A * B                           │ │
│  │   1011   │    DIV    │ A / B                           │ │
│  └─────────────────────────────────────────────────────────┘ │
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │                  STATUS FLAGS                           │ │
│  │                                                         │ │
│  │  Z (Zero): Set if result is zero                       │ │
│  │  N (Negative): Set if result is negative               │ │
│  │  C (Carry): Set if carry out from MSB                  │ │
│  │  V (Overflow): Set if signed overflow occurs           │ │
│  │                                                         │ │
│  │  Example: ADD operation                                │ │
│  │  A = 0x7FFFFFFF (2,147,483,647)                        │ │
│  │  B = 0x00000001 (1)                                    │ │
│  │  Result = 0x80000000 (-2,147,483,648)                  │ │
│  │  Flags: Z=0, N=1, C=0, V=1                            │ │
│  └─────────────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────────┘
```

## 5. I/O System and Bus Structure

### I/O System Organization
```
┌─────────────────────────────────────────────────────────────┐
│                    I/O SYSTEM                              │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  Input/Output System: Interface between CPU and            │
│  external devices for data transfer                        │
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │                I/O SYSTEM STRUCTURE                     │ │
│  │                                                         │ │
│  │      CPU                    Memory                      │ │
│  │  ┌─────────┐              ┌─────────┐                   │ │
│  │  │         │──────────────│         │                   │ │
│  │  │         │   System Bus │         │                   │ │
│  │  │         │              │         │                   │ │
│  │  └─────────┘              └─────────┘                   │ │
│  │       │                        │                       │ │
│  │       └────────────┬───────────┘                       │ │
│  │                    │                                   │ │
│  │                    ▼                                   │ │
│  │            ┌──────────────────┐                        │ │
│  │            │   I/O INTERFACE  │                        │ │
│  │            │                  │                        │ │
│  │            │ ┌──────────────┐ │                        │ │
│  │            │ │I/O CONTROLLER│ │                        │ │
│  │            │ └──────────────┘ │                        │ │
│  │            │ ┌──────────────┐ │                        │ │
│  │            │ │    BUFFER    │ │                        │ │
│  │            │ └──────────────┘ │                        │ │
│  │            │ ┌──────────────┐ │                        │ │
│  │            │ │STATUS/CONTROL│ │                        │ │
│  │            │ │  REGISTERS   │ │                        │ │
│  │            │ └──────────────┘ │                        │ │
│  │            └──────────────────┘                        │ │
│  │                    │                                   │ │
│  │                    ▼                                   │ │
│  │       ┌─────────┐ ┌─────────┐ ┌─────────┐              │ │
│  │       │KEYBOARD │ │MONITOR  │ │PRINTER  │              │ │
│  │       │         │ │         │ │         │              │ │
│  │       └─────────┘ └─────────┘ └─────────┘              │ │
│  └─────────────────────────────────────────────────────────┘ │
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │                I/O TRANSFER METHODS                     │ │
│  │                                                         │ │
│  │  1. PROGRAMMED I/O:                                    │ │
│  │     • CPU directly controls I/O operations             │ │
│  │     • CPU waits for I/O completion                     │ │
│  │     • Simple but inefficient                           │ │
│  │                                                         │ │
│  │  2. INTERRUPT-DRIVEN I/O:                              │ │
│  │     • I/O device interrupts CPU when ready             │ │
│  │     • CPU can do other work while waiting              │ │
│  │     • More efficient than programmed I/O               │ │
│  │                                                         │ │
│  │  3. DIRECT MEMORY ACCESS (DMA):                        │ │
│  │     • I/O controller directly accesses memory          │ │
│  │     • CPU involvement minimal                          │ │
│  │     • Highest efficiency for large data transfers      │ │
│  └─────────────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────────┘
```

### Bus Structure
```
┌─────────────────────────────────────────────────────────────┐
│                     BUS STRUCTURE                          │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  Bus: A shared communication pathway that connects         │
│  multiple devices and allows data transfer                 │
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │                THREE-BUS SYSTEM                         │ │
│  │                                                         │ │
│  │        CPU           Memory         I/O Devices        │ │
│  │    ┌─────────┐    ┌─────────┐     ┌─────────┐          │ │
│  │    │         │    │         │     │         │          │ │
│  │    │   ALU   │    │  RAM    │     │Interface│          │ │
│  │    │         │    │         │     │         │          │ │
│  │    │Control  │    │  ROM    │     │Controller│         │ │
│  │    │  Unit   │    │         │     │         │          │ │
│  │    └─────────┘    └─────────┘     └─────────┘          │ │
│  │         │              │               │               │ │
│  │         ▼              ▼               ▼               │ │
│  │    ┌─────────────────────────────────────────────────┐  │ │
│  │    │           ADDRESS BUS (32 bits)                │  │ │
│  │    │    Carries memory addresses and I/O ports      │  │ │
│  │    └─────────────────────────────────────────────────┘  │ │
│  │                                                         │ │
│  │    ┌─────────────────────────────────────────────────┐  │ │
│  │    │            DATA BUS (32 bits)                  │  │ │
│  │    │     Carries data between components             │  │ │
│  │    └─────────────────────────────────────────────────┘  │ │
│  │                                                         │ │
│  │    ┌─────────────────────────────────────────────────┐  │ │
│  │    │           CONTROL BUS (varies)                  │  │ │
│  │    │   READ, write, interrupt, clock signals        │  │ │
│  │    └─────────────────────────────────────────────────┘  │ │
│  └─────────────────────────────────────────────────────────┘ │
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │                  BUS CHARACTERISTICS                    │ │
│  │                                                         │ │
│  │  Address Bus:                                          │ │
│  │  • Width determines memory addressing capability       │ │
│  │  • 32-bit address bus = 4GB addressable space         │ │
│  │  • Unidirectional (CPU to memory/I/O)                 │ │
│  │                                                         │ │
│  │  Data Bus:                                             │ │
│  │  • Width determines data transfer rate                 │ │
│  │  • 32-bit data bus transfers 4 bytes per cycle        │ │
│  │  • Bidirectional (CPU ↔ memory/I/O)                   │ │
│  │                                                         │ │
│  │  Control Bus:                                          │ │
│  │  • READ: Enable read operation                         │ │
│  │  • WRITE: Enable write operation                       │ │
│  │  • CLOCK: Synchronization signal                       │ │
│  │  • INTERRUPT: Request CPU attention                    │ │
│  │  • RESET: Initialize system                            │ │
│  │  • READY: Device ready for operation                   │ │
│  └─────────────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────────┘
```

## 6. Program Counter and Register Transfer Language

### Program Counter (PC)
```
┌─────────────────────────────────────────────────────────────┐
│                    PROGRAM COUNTER                         │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  Program Counter: Register that holds the address of       │
│  the next instruction to be executed                       │
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │               PC OPERATION                              │ │
│  │                                                         │ │
│  │  Memory                    CPU                          │ │
│  │  ┌─────────────────┐    ┌─────────────────┐             │ │
│  │  │ 0x1000: LOAD R1 │    │ PC: 0x1000      │             │ │
│  │  │ 0x1004: ADD R2  │    │                 │             │ │
│  │  │ 0x1008: STORE R3│    │ IR: LOAD R1     │             │ │
│  │  │ 0x100C: JMP Loop│    │                 │             │ │
│  │  │ 0x1010: NOP     │    │                 │             │ │
│  │  └─────────────────┘    └─────────────────┘             │ │
│  │                                                         │ │
│  │  Instruction Fetch Cycle:                              │ │
│  │  1. MAR ← PC         (Load address into MAR)           │ │
│  │  2. IR ← M[MAR]      (Fetch instruction from memory)   │ │
│  │  3. PC ← PC + 4      (Increment PC for next instr)     │ │
│  │  4. Decode IR        (Decode current instruction)      │ │
│  │  5. Execute IR       (Execute current instruction)     │ │
│  └─────────────────────────────────────────────────────────┘ │
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │               PC MODIFICATIONS                          │ │
│  │                                                         │ │
│  │  Sequential Execution:                                 │ │
│  │  PC ← PC + 4 (for 32-bit instructions)                │ │
│  │                                                         │ │
│  │  Branch Instructions:                                  │ │
│  │  if (condition) PC ← PC + offset                       │ │
│  │  else PC ← PC + 4                                      │ │
│  │                                                         │ │
│  │  Jump Instructions:                                    │ │
│  │  PC ← target_address                                   │ │
│  │                                                         │ │
│  │  Subroutine Call:                                      │ │
│  │  Stack ← PC + 4 (save return address)                 │ │
│  │  PC ← subroutine_address                              │ │
│  │                                                         │ │
│  │  Subroutine Return:                                    │ │
│  │  PC ← Stack (restore return address)                  │ │
│  │                                                         │ │
│  │  Interrupt Handling:                                   │ │
│  │  Stack ← PC (save current PC)                         │ │
│  │  PC ← interrupt_vector                                 │ │
│  └─────────────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────────┘
```

### Register Transfer Language (RTL)
```
┌─────────────────────────────────────────────────────────────┐
│             REGISTER TRANSFER LANGUAGE                     │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  RTL: Symbolic notation to describe data transfer          │
│  between registers and memory locations                    │
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │                 RTL NOTATION                            │ │
│  │                                                         │ │
│  │  Basic Transfer:                                       │ │
│  │  R1 ← R2      (Contents of R2 transferred to R1)       │ │
│  │                                                         │ │
│  │  Conditional Transfer:                                 │ │
│  │  if (T) R1 ← R2   (Transfer only if T is true)         │ │
│  │                                                         │ │
│  │  Memory Transfer:                                      │ │
│  │  R1 ← M[R2]   (Load from memory address in R2)        │ │
│  │  M[R1] ← R2   (Store R2 to memory address in R1)      │ │
│  │                                                         │ │
│  │  Arithmetic Operations:                                │ │
│  │  R1 ← R2 + R3     (Addition)                          │ │
│  │  R1 ← R2 - R3     (Subtraction)                       │ │
│  │  R1 ← R2 * R3     (Multiplication)                    │ │
│  │  R1 ← R2 / R3     (Division)                          │ │
│  │                                                         │ │
│  │  Logical Operations:                                   │ │
│  │  R1 ← R2 ∧ R3     (AND operation)                     │ │
│  │  R1 ← R2 ∨ R3     (OR operation)                      │ │
│  │  R1 ← R2 ⊕ R3     (XOR operation)                     │ │
│  │  R1 ← R2'         (NOT operation)                     │ │
│  └─────────────────────────────────────────────────────────┘ │
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │               RTL EXAMPLES                              │ │
│  │                                                         │ │
│  │  LOAD Instruction: LOAD R1, 100(R2)                   │ │
│  │  RTL: MAR ← R2 + 100                                  │ │
│  │       MDR ← M[MAR]                                     │ │
│  │       R1 ← MDR                                         │ │
│  │                                                         │ │
│  │  STORE Instruction: STORE R1, 200(R2)                 │ │
│  │  RTL: MAR ← R2 + 200                                  │ │
│  │       MDR ← R1                                         │ │
│  │       M[MAR] ← MDR                                     │ │
│  │                                                         │ │
│  │  ADD Instruction: ADD R1, R2, R3                      │ │
│  │  RTL: R1 ← R2 + R3                                    │ │
│  │                                                         │ │
│  │  BRANCH Instruction: BEQ R1, R2, LABEL                │ │
│  │  RTL: if (R1 = R2) PC ← PC + offset                   │ │
│  │       else PC ← PC + 4                                 │ │
│  │                                                         │ │
│  │  JUMP Instruction: JUMP ADDRESS                       │ │
│  │  RTL: PC ← ADDRESS                                     │ │
│  └─────────────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────────┘
```

## 7. Addressing Modes

### Overview of Addressing Modes
```
┌─────────────────────────────────────────────────────────────┐
│                   ADDRESSING MODES                         │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  Addressing Mode: Method of specifying operands in         │
│  instructions (how to find data for operations)            │
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │              IMMEDIATE ADDRESSING                       │ │
│  │                                                         │ │
│  │  Operand is part of the instruction itself             │ │
│  │                                                         │ │
│  │  Instruction: ADDI R1, R2, #100                        │ │
│  │  Operation: R1 ← R2 + 100                              │ │
│  │                                                         │ │
│  │  ┌─────────────────────────────────────────────────────┐ │ │
│  │  │ Instruction │        100         │  R2  │  R1  │   │ │ │
│  │  │   OpCode    │   Immediate Value  │ Src  │ Dest │   │ │ │
│  │  └─────────────────────────────────────────────────────┘ │ │
│  │                                                         │ │
│  │  Advantages: Fast (no memory access for operand)       │ │
│  │  Disadvantages: Limited range of values                │ │
│  └─────────────────────────────────────────────────────────┘ │
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │               DIRECT ADDRESSING                         │ │
│  │                                                         │ │
│  │  Operand address is specified in instruction           │ │
│  │                                                         │ │
│  │  Instruction: LOAD R1, 1000                            │ │
│  │  Operation: R1 ← M[1000]                               │ │
│  │                                                         │ │
│  │  Memory:                                               │ │
│  │  ┌───────────┬─────────┐                               │ │
│  │  │ Address   │  Data   │                               │ │
│  │  ├───────────┼─────────┤                               │ │
│  │  │   1000    │   25    │ ← Operand location            │ │
│  │  │   1004    │   30    │                               │ │
│  │  │   1008    │   45    │                               │ │
│  │  └───────────┴─────────┘                               │ │
│  │                                                         │ │
│  │  Effective Address = 1000                              │ │
│  │  Operand = M[1000] = 25                                │ │
│  └─────────────────────────────────────────────────────────┘ │
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │              INDIRECT ADDRESSING                        │ │
│  │                                                         │ │
│  │  Instruction contains address of address of operand    │ │
│  │                                                         │ │
│  │  Instruction: LOAD R1, @1000                           │ │
│  │  Operation: R1 ← M[M[1000]]                            │ │
│  │                                                         │ │
│  │  Memory:                                               │ │
│  │  ┌───────────┬─────────┐                               │ │
│  │  │ Address   │  Data   │                               │ │
│  │  ├───────────┼─────────┤                               │ │
│  │  │   1000    │  2000   │ ← Points to actual data       │ │
│  │  │   1004    │   30    │                               │ │
│  │  │   2000    │   75    │ ← Actual operand              │ │
│  │  │   2004    │   80    │                               │ │
│  │  └───────────┴─────────┘                               │ │
│  │                                                         │ │
│  │  Effective Address = M[1000] = 2000                    │ │
│  │  Operand = M[2000] = 75                                │ │
│  └─────────────────────────────────────────────────────────┘ │
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │             DISPLACEMENT ADDRESSING                     │ │
│  │                                                         │ │
│  │  Effective address = Base + Displacement            │ │
│  │                                                         │ │
│  │  Instruction: LOAD R1, 100(R2)                         │ │
│  │  Operation: R1 ← M[R2 + 100]                           │ │
│  │                                                         │ │
│  │  Register R2: [00000000000000000000010000000000] (1024) │ │
│  │  Displacement: 100                                     │ │
│  │                                                         │ │
│  │  Effective Address = 1024 + 100 = 1124                 │ │
│  │  Operand = M[1124]                                     │ │
│  │                                                         │ │
│  │  Useful for: Arrays, Stack operations, Local variables │ │
│  └─────────────────────────────────────────────────────────┘ │
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │               INDEXED ADDRESSING                        │ │
│  │                                                         │ │
│  │  Effective address = Base + Index                      │ │
│  │                                                         │ │
│  │  Instruction: LOAD R1, Array(R2)                       │ │
│  │  Operation: R1 ← M[Array_Base + R2]                    │ │
│  │                                                         │ │
│  │  Array_Base: 2000                                      │ │
│  │  Index R2: 12 (3rd element, each element 4 bytes)     │ │
│  │                                                         │ │
│  │  Effective Address = 2000 + 12 = 2012                  │ │
│  │                                                         │ │
│  │  Array Layout:                                         │ │
│  │  ┌────────┬──────────┬─────────┐                       │ │
│  │  │ 2000   │ 2004     │ 2008    │ ...                   │ │
│  │  │ A[0]   │ A[1]     │ A[2]    │                       │ │
│  │  └────────┴──────────┴─────────┘                       │ │
│  │                      ↑                                 │ │
│  │                   Index=2                              │ │
│  └─────────────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────────┘
```

## 8. Control Unit Organization

### Basic Concept of Instructions
```
┌─────────────────────────────────────────────────────────────┐
│                 INSTRUCTION CONCEPTS                       │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  Instruction: A command that tells the CPU what operation  │
│  to perform on specified data                              │
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │              INSTRUCTION COMPONENTS                     │ │
│  │                                                         │ │
│  │  ┌─────────────────────────────────────────────────────┐ │ │
│  │  │                OPCODE                               │ │ │
│  │  │                                                     │ │ │
│  │  │  • Specifies the operation to be performed         │ │ │
│  │  │  • Examples: ADD, SUB, LOAD, STORE, JUMP           │ │ │
│  │  │  • Determines control signals needed               │ │ │
│  │  └─────────────────────────────────────────────────────┘ │ │
│  │                                                         │ │
│  │  ┌─────────────────────────────────────────────────────┐ │ │
│  │  │               OPERANDS                              │ │ │
│  │  │                                                     │ │ │
│  │  │  • Data or addresses on which operation acts       │ │ │
│  │  │  • Can be registers, memory locations, or values   │ │ │
│  │  │  • Number varies by instruction type               │ │ │
│  │  └─────────────────────────────────────────────────────┘ │ │
│  │                                                         │ │
│  │  Example: ADD R1, R2, R3                               │ │
│  │  ┌─────────┬─────────┬─────────┬─────────┐              │ │
│  │  │  ADD    │   R2    │   R3    │   R1    │              │ │
│  │  │ OpCode  │ Source1 │ Source2 │  Dest   │              │ │
│  │  └─────────┴─────────┴─────────┴─────────┘              │ │
│  └─────────────────────────────────────────────────────────┘ │
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │              INSTRUCTION EXECUTION                      │ │
│  │                                                         │ │
│  │  1. FETCH: Get instruction from memory                 │ │
│  │     • PC → MAR (Program Counter to Memory Address)     │ │
│  │     • M[MAR] → IR (Memory to Instruction Register)     │ │
│  │     • PC + 4 → PC (Increment Program Counter)          │ │
│  │                                                         │ │
│  │  2. DECODE: Interpret instruction                      │ │
│  │     • Extract opcode and operands                      │ │
│  │     • Generate control signals                         │ │
│  │     • Identify required resources                      │ │
│  │                                                         │ │
│  │  3. EXECUTE: Perform operation                         │ │
│  │     • Access operands from registers/memory            │ │
│  │     • Perform ALU operations                           │ │
│  │     • Store results                                    │ │
│  │                                                         │ │
│  │  4. WRITEBACK: Store results (if needed)               │ │
│  │     • Write results to destination register            │ │
│  │     • Update status flags                              │ │
│  │     • Handle exceptions                                │ │
│  └─────────────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────────┘
```

### Instruction Types
```
┌─────────────────────────────────────────────────────────────┐
│                   INSTRUCTION TYPES                        │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │              DATA MOVEMENT                              │ │
│  │                                                         │ │
│  │  Transfer data between registers and memory             │ │
│  │                                                         │ │
│  │  • LOAD R1, 1000      : R1 ← M[1000]                  │ │
│  │  • STORE R1, 2000     : M[2000] ← R1                  │ │
│  │  • MOVE R1, R2        : R1 ← R2                       │ │
│  │  • LDI R1, #100       : R1 ← 100 (Load Immediate)     │ │
│  │  └─────────────────────────────────────────────────────────┘ │
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │              ARITHMETIC                                 │ │
│  │                                                         │ │
│  │  Perform mathematical operations                       │ │
│  │                                                         │ │
│  │  • ADD R1, R2, R3     : R1 ← R2 + R3                  │ │
│  │  • SUB R1, R2, R3     : R1 ← R2 - R3                  │ │
│  │  • MUL R1, R2, R3     : R1 ← R2 × R3                  │ │
│  │  • DIV R1, R2, R3     : R1 ← R2 ÷ R3                  │ │
│  │  • INC R1            : R1 ← R1 + 1                    │ │
│  │  • DEC R1            : R1 ← R1 - 1                    │ │
│  │  └─────────────────────────────────────────────────────────┘ │
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │                LOGICAL                                  │ │
│  │                                                         │ │
│  │  Perform bitwise logical operations                    │ │
│  │                                                         │ │
│  │  • AND R1, R2, R3     : R1 ← R2 & R3                  │ │
│  │  • OR R1, R2, R3      : R1 ← R2 | R3                  │ │
│  │  • XOR R1, R2, R3     : R1 ← R2 ⊕ R3                  │ │
│  │  • NOT R1, R2         : R1 ← ~R2                      │ │
│  │  • SHL R1, R2, #3     : R1 ← R2 << 3                  │ │
│  │  • SHR R1, R2, #2     : R1 ← R2 >> 2                  │ │
│  │  └─────────────────────────────────────────────────────────┘ │
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │              CONTROL FLOW                              │ │
│  │                                                         │ │
│  │  Change program execution sequence                     │ │
│  │                                                         │ │
│  │  • JMP LABEL          : PC ← LABEL                     │ │
│  │  • BEQ R1, R2, LABEL  : if R1=R2 then PC←LABEL        │ │
│  │  • BNE R1, R2, LABEL  : if R1≠R2 then PC←LABEL        │ │
│  │  • CALL PROC          : Stack←PC+4, PC←PROC            │ │
│  │  • RET                : PC←Stack                       │ │
│  │  • HALT               : Stop execution                 │ │
│  └─────────────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────────┘
```

### Fetch and Execution Cycle
```
┌─────────────────────────────────────────────────────────────┐
│                FETCH-DECODE-EXECUTE CYCLE                  │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │                   FETCH PHASE                           │ │
│  │                                                         │ │
│  │  T0: MAR ← PC                                          │ │
│  │      (Transfer PC contents to Memory Address Register) │ │
│  │                                                         │ │
│  │  T1: MDR ← M[MAR], PC ← PC + 4                         │ │
│  │      (Read instruction from memory, increment PC)      │ │
│  │                                                         │ │
│  │  T2: IR ← MDR                                          │ │
│  │      (Transfer instruction to Instruction Register)    │ │
│  │                                                         │ │
│  │  ┌───────────────────────────────────────────────────┐   │ │
│  │  │     Memory          CPU                           │   │ │
│  │  │  ┌─────────────┐ ┌─────────────┐                  │   │ │
│  │  │  │    1000     │ │  PC: 1000   │                  │   │ │
│  │  │  │    1004     │ │  MAR: 1000  │                  │   │ │
│  │  │  │    1008     │ │  MDR: inst  │                  │   │ │
│  │  │  │    ...      │ │  IR: inst   │                  │   │ │
│  │  │  └─────────────┘ └─────────────┘                  │   │ │
│  │  └───────────────────────────────────────────────────┘   │ │
│  └─────────────────────────────────────────────────────────┘ │
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │                  DECODE PHASE                           │ │
│  │                                                         │ │
│  │  T3: OpCode ← IR[31:26]                                │ │
│  │      (Extract operation code)                          │ │
│  │                                                         │ │
│  │  T4: Operands ← IR[25:0]                               │ │
│  │      (Extract operand fields)                          │ │
│  │                                                         │ │
│  │  T5: Generate Control Signals                          │ │
│  │      (Determine required micro-operations)             │ │
│  │                                                         │ │
│  │  Control Unit determines:                              │ │
│  │  • Which registers to use                              │ │
│  │  • ALU operation required                              │ │
│  │  • Memory access needed                                │ │
│  │  • Next instruction address                            │ │
│  └─────────────────────────────────────────────────────────┘ │
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │                 EXECUTE PHASE                           │ │
│  │                                                         │ │
│  │  Example: ADD R1, R2, R3                               │ │
│  │                                                         │ │
│  │  T6: A ← R2, B ← R3                                    │ │
│  │      (Get operands from registers)                     │ │
│  │                                                         │ │
│  │  T7: ALU_OUT ← A + B                                   │ │
│  │      (Perform addition in ALU)                         │ │
│  │                                                         │ │
│  │  T8: R1 ← ALU_OUT                                      │ │
│  │      (Store result in destination register)            │ │
│  │                                                         │ │
│  │  T9: Update Status Flags                               │ │
│  │      (Set Z, N, C, V flags based on result)            │ │
│  └─────────────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────────┘
```

### Hardwired Control Unit
```
┌─────────────────────────────────────────────────────────────┐
│                 HARDWIRED CONTROL UNIT                    │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  Hardwired Control: Uses fixed logic circuits to generate  │
│  control signals directly from instruction opcode          │
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │              HARDWIRED STRUCTURE                        │ │
│  │                                                         │ │
│  │  Instruction Register (IR)                             │ │
│  │  ┌─────────────────────────────────────┐                │ │
│  │  │ OpCode │ Operands │    Flags       │                │ │
│  │  └─────────────────────────────────────┘                │ │
│  │       │                                                 │ │
│  │       ▼                                                 │ │
│  │  ┌─────────────────────────────────────┐                │ │
│  │  │        INSTRUCTION DECODER           │                │ │
│  │  │                                     │                │ │
│  │  │  ┌────────┐ ┌────────┐ ┌────────┐   │                │ │
│  │  │  │ AND    │ │  OR    │ │  NOT   │   │                │ │
│  │  │  │ Gates  │ │ Gates  │ │ Gates  │   │                │ │
│  │  │  └────────┘ └────────┘ └────────┘   │                │ │
│  │  └─────────────────────────────────────┘                │ │
│  │                       │                                 │ │
│  │                       ▼                                 │ │
│  │  ┌─────────────────────────────────────┐                │ │
│  │  │       CONTROL SIGNAL GENERATOR      │                │ │
│  │  │                                     │                │ │
│  │  │  RegWrite  MemRead  MemWrite  ALUOp │                │ │
│  │  │     │         │        │       │    │                │ │
│  │  └─────┼─────────┼────────┼───────┼────┘                │ │
│  │        │         │        │       │                     │ │
│  │        ▼         ▼        ▼       ▼                     │ │
│  │   ┌────────┐ ┌────────┐ ┌────────┐ ┌────────┐           │ │
│  │   │Register│ │ Memory │ │ Memory │ │  ALU   │           │ │
│  │   │  File  │ │  Read  │ │ Write  │ │Control │           │ │
│  │   └────────┘ └────────┘ └────────┘ └────────┘           │ │
│  └─────────────────────────────────────────────────────────┘ │
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │            ADVANTAGES & DISADVANTAGES                   │ │
│  │                                                         │ │
│  │  Advantages:                                           │ │
│  │  • Fast operation (direct logic)                       │ │
│  │  • No memory access for control                        │ │
│  │  • Simple timing control                               │ │
│  │  • Lower cost for simple processors                    │ │
│  │                                                         │ │
│  │  Disadvantages:                                        │ │
│  │  • Difficult to modify or debug                        │ │
│  │  • Complex logic for complex instructions              │ │
│  │  • Requires complete redesign for changes              │ │
│  │  • Fixed instruction set                               │ │
│  └─────────────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────────┘
```

### Microprogrammed Control Unit
```
┌─────────────────────────────────────────────────────────────┐
│               MICROPROGRAMMED CONTROL UNIT                 │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  Microprogrammed Control: Uses stored microinstructions    │
│  in control memory to generate control signals             │
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │           MICROPROGRAMMED STRUCTURE                     │ │
│  │                                                         │ │
│  │  Instruction Register                                  │ │
│  │  ┌─────────────────────────────────────┐                │ │
│  │  │ OpCode │ Operands │    Flags       │                │ │
│  │  └─────────────────────────────────────┘                │ │
│  │       │                                                 │ │
│  │       ▼                                                 │ │
│  │  ┌─────────────────────────────────────┐                │ │
│  │  │      MICROPROGRAM COUNTER (μPC)     │                │ │
│  │  │           Address Generator         │                │ │
│  │  └─────────────────────────────────────┘                │ │
│  │                       │                                 │ │
│  │                       ▼                                 │ │
│  │  ┌─────────────────────────────────────┐                │ │
│  │  │        CONTROL MEMORY               │                │ │
│  │  │                                     │                │ │
│  │  │  0000: │RegA│RegB│ALU │Mem│Next│    │                │ │
│  │  │  0001: │ 01 │ 10 │ADD │RD │0010│    │                │ │
│  │  │  0002: │ 10 │ 00 │OR  │WR │0003│    │                │ │
│  │  │  0003: │ 11 │ 01 │AND │-- │0000│    │                │ │
│  │  │  ....  │    │    │    │   │    │    │                │ │
│  │  └─────────────────────────────────────┘                │ │
│  │                       │                                 │ │
│  │                       ▼                                 │ │
│  │  ┌─────────────────────────────────────┐                │ │
│  │  │    MICROINSTRUCTION REGISTER        │                │ │
│  │  │         (Control Word)              │                │ │
│  │  └─────────────────────────────────────┘                │ │
│  │                       │                                 │ │
│  │                       ▼                                 │ │
│  │       Control Signals to CPU Components                │ │
│  └─────────────────────────────────────────────────────────┘ │
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │               MICROPROGRAM EXECUTION                    │ │
│  │                                                         │ │
│  │  1. Fetch machine instruction into IR                  │ │
│  │  2. OpCode → μPC (Load starting microaddress)          │ │
│  │  3. Read microinstruction from control memory          │ │
│  │  4. Execute microinstruction (generate signals)        │ │
│  │  5. μPC ← Next Address field                           │ │
│  │  6. Repeat steps 3-5 until instruction complete        │ │
│  │                                                         │ │
│  │  Example: ADD R1, R2, R3 microprogram                  │ │
│  │  μAddr │ Control Word                   │ Next          │ │
│  │  ──────┼────────────────────────────────┼──────         │ │
│  │  0010  │ RegA=R2, RegB=R3, ALU=ADD     │ 0011          │ │
│  │  0011  │ RegDest=R1, RegWrite=1         │ 0000          │ │
│  └─────────────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────────┘
```

### Microinstruction Formats
```
┌─────────────────────────────────────────────────────────────┐
│               MICROINSTRUCTION FORMATS                     │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │            HORIZONTAL MICROINSTRUCTION                  │ │
│  │                                                         │ │
│  │  Each bit controls a specific control signal            │ │
│  │                                                         │ │
│  │  64-bit Microinstruction Example:                      │ │
│  │  ┌──┬──┬──┬───┬───┬───┬────┬────┬─────┬──────┬────────┐  │ │
│  │  │RegA│RegB│Dest│ALU│Mem│Bus│RegW│MemR│MemW │Branch│Next│  │ │
│  │  │ 3  │ 3 │ 3  │ 4 │ 2 │ 2 │ 1  │ 1  │ 1   │  2   │ 16 │  │ │
│  │  └──┴──┴──┴───┴───┴───┴────┴────┴─────┴──────┴────────┘  │ │
│  │                                                         │ │
│  │  Field Meanings:                                       │ │
│  │  • RegA/RegB: Source register selectors               │ │
│  │  • Dest: Destination register selector                │ │
│  │  • ALU: ALU operation code                             │ │
│  │  • Mem: Memory operation control                       │ │
│  │  • Bus: Bus control signals                            │ │
│  │  • RegW: Register write enable                         │ │
│  │  • MemR/MemW: Memory read/write enables                │ │
│  │  • Branch: Conditional branch control                  │ │
│  │  • Next: Address of next microinstruction              │ │
│  │                                                         │ │
│  │  Advantages: Simple decoding, fast execution           │ │
│  │  Disadvantages: Long instruction word, wasteful        │ │
│  └─────────────────────────────────────────────────────────┘ │
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │             VERTICAL MICROINSTRUCTION                   │ │
│  │                                                         │ │
│  │  Encoded format with operation codes                   │ │
│  │                                                         │ │
│  │  32-bit Microinstruction Example:                      │ │
│  │  ┌────────────┬─────────────┬──────────────────────────┐ │ │
│  │  │  Op Code   │  Operands   │      Next Address        │ │ │
│  │  │   8 bits   │   8 bits    │       16 bits            │ │ │
│  │  └────────────┴─────────────┴──────────────────────────┘ │ │
│  │                                                         │ │
│  │  Operation Codes:                                      │ │
│  │  00000001: Load register from memory                   │ │
│  │  00000010: Store register to memory                    │ │
│  │  00000100: Arithmetic operation                        │ │
│  │  00001000: Logic operation                             │ │
│  │  00010000: Branch operation                            │ │
│  │                                                         │ │
│  │  Advantages: Shorter instruction, efficient encoding   │ │
│  │  Disadvantages: Requires decoder, slower execution     │ │
│  └─────────────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────────┘
```

### Microprogram Sequencer and Control Memory
```
┌─────────────────────────────────────────────────────────────┐
│           MICROPROGRAM SEQUENCER & CONTROL MEMORY          │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │              MICROPROGRAM SEQUENCER                     │ │
│  │                                                         │ │
│  │  Controls the sequence of microinstruction execution   │ │
│  │                                                         │ │
│  │  ┌─────────────────────────────────────────────────────┐ │ │
│  │  │           SEQUENCER COMPONENTS                      │ │ │
│  │  │                                                     │ │ │
│  │  │  ┌─────────────┐    ┌─────────────┐                │ │ │
│  │  │  │Microprogram │    │   Mapping   │                │ │ │
│  │  │  │  Counter    │    │    ROM      │                │ │ │
│  │  │  │   (μPC)     │    │             │                │ │ │
│  │  │  └─────────────┘    └─────────────┘                │ │ │
│  │  │         │                    │                     │ │ │
│  │  │         ▼                    ▼                     │ │ │
│  │  │  ┌─────────────────────────────────┐               │ │ │
│  │  │  │          MUX                    │               │ │ │
│  │  │  │                                 │               │ │ │
│  │  │  │ Inputs:                         │               │ │ │
│  │  │  │ • μPC + 1 (Sequential)          │               │ │ │
│  │  │  │ • Next field (Branch)           │               │ │ │
│  │  │  │ • Mapping ROM (New instruction) │               │ │ │
│  │  │  │ • Subroutine return address     │               │ │ │
│  │  │  └─────────────────────────────────┘               │ │ │
│  │  │                    │                               │ │ │
│  │  │                    ▼                               │ │ │
│  │  │              Control Memory                        │ │ │
│  │  └─────────────────────────────────────────────────────┘ │ │
│  │                                                         │ │
│  │  Sequencing Operations:                                │ │
│  │  • Sequential: μPC ← μPC + 1                          │ │
│  │  • Branch: μPC ← Next Address field                   │ │
│  │  • Conditional: μPC ← condition ? branch : μPC+1      │ │
│  │  • Jump: μPC ← Mapping ROM[OpCode]                    │ │
│  └─────────────────────────────────────────────────────────┘ │
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │                CONTROL MEMORY                           │ │
│  │                                                         │ │
│  │  Fast memory that stores microinstructions             │ │
│  │                                                         │ │
│  │  ┌─────────────────────────────────────────────────────┐ │ │
│  │  │              MEMORY ORGANIZATION                    │ │ │
│  │  │                                                     │ │ │
│  │  │  Address │ Microinstruction                         │ │ │
│  │  │  ────────┼─────────────────────────────────────     │ │ │
│  │  │   0000   │ [Control Word for NOP]                  │ │ │
│  │  │   0001   │ [Control Word for LOAD - Phase 1]       │ │ │
│  │  │   0002   │ [Control Word for LOAD - Phase 2]       │ │ │
│  │  │   0003   │ [Control Word for STORE - Phase 1]      │ │ │
│  │  │   0004   │ [Control Word for STORE - Phase 2]      │ │ │
│  │  │   0005   │ [Control Word for ADD - Phase 1]        │ │ │
│  │  │   0006   │ [Control Word for ADD - Phase 2]        │ │ │
│  │  │   ....   │ [More microinstructions]                │ │ │
│  │  │                                                     │ │ │
│  │  │  Characteristics:                                   │ │ │
│  │  │  • High speed (ROM or fast RAM)                    │ │ │
│  │  │  • Word size = microinstruction width              │ │ │
│  │  │  • Capacity = number of microinstructions needed   │ │ │
│  │  │  • Typical size: 1K to 4K words                    │ │ │
│  │  └─────────────────────────────────────────────────────┘ │ │
│  └─────────────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────────┘
```

## 10. Summary and Quick Reference

### Key Concepts Summary
```
┌─────────────────────────────────────────────────────────────┐
│                    UNIT I SUMMARY                          │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │               COMPUTER ORGANIZATION                     │ │
│  │                                                         │ │
│  │  Basic Structure:                                      │ │
│  │  • Von Neumann Architecture (CPU, Memory, I/O)         │ │
│  │  • CPU Components (ALU, Control Unit, Registers)       │ │
│  │  • Memory Hierarchy (Registers, Cache, RAM, Storage)   │ │
│  │                                                         │ │
│  │  CPU Architecture:                                     │ │
│  │  • Register Organization (General purpose, Special)    │ │
│  │  • ALU Operations (Arithmetic, Logic, Shift)           │ │
│  │  • Control Word (Microoperation specification)         │ │
│  │                                                         │ │
│  │  Stack Organization:                                   │ │
│  │  • LIFO structure for temporary storage                │ │
│  │  • Used for subroutines, interrupts, expressions      │ │
│  │  • Operations: PUSH, POP                               │ │
│  └─────────────────────────────────────────────────────────┘ │
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │              INSTRUCTION PROCESSING                     │ │
│  │                                                         │ │
│  │  Instruction Formats:                                  │ │
│  │  • R-Type: Register operations                         │ │
│  │  • I-Type: Immediate and Load/Store                    │ │
│  │  • J-Type: Jump operations                             │ │
│  │                                                         │ │
│  │  Addressing Modes:                                     │ │
│  │  • Immediate, Direct, Indirect                         │ │
│  │  • Register, Register Indirect                         │ │
│  │  • Displacement, Indexed                               │ │
│  │                                                         │ │
│  │  Execution Cycle:                                      │ │
│  │  • Fetch → Decode → Execute → Writeback                │ │
│  │  • Program Counter management                          │ │
│  │  • Register Transfer Language notation                 │ │
│  └─────────────────────────────────────────────────────────┘ │
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │               CONTROL UNIT DESIGN                      │ │
│  │                                                         │ │
│  │  Hardwired Control:                                    │ │
│  │  • Fixed logic circuits                                │ │
│  │  • Fast execution, difficult to modify                 │ │
│  │  • Direct opcode to control signal mapping             │ │
│  │                                                         │ │
│  │  Microprogrammed Control:                              │ │
│  │  • Stored microinstructions in control memory          │ │
│  │  • Flexible, easier to modify                          │ │
│  │  • Microprogram sequencer for control flow             │ │
│  │                                                         │ │
│  │  Microinstruction Formats:                             │ │
│  │  • Horizontal: Direct control, longer words            │ │
│  │  • Vertical: Encoded control, shorter words            │ │
│  └─────────────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────────┘
```

### Important Formulas and Values
```
┌─────────────────────────────────────────────────────────────┐
│               FORMULAS AND KEY VALUES                      │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  Memory Addressing:                                        │
│  • Address Space = 2^n (where n = address bus width)       │
│  • 32-bit address bus = 2^32 = 4 GB addressable space     │
│                                                             │
│  Instruction Execution Time:                               │
│  • Hardwired CU: T = Clock_Period × Clock_Cycles           │
│  • Microprogrammed CU: T = μClock_Period × μInstructions   │
│                                                             │
│  Stack Operations:                                         │
│  • PUSH: SP ← SP - 1, M[SP] ← Data                        │
│  • POP: Data ← M[SP], SP ← SP + 1                         │
│                                                             │
│  Program Counter Updates:                                  │
│  • Sequential: PC ← PC + 4 (32-bit instructions)          │
│  • Branch: PC ← PC + offset (if condition true)           │
│  • Jump: PC ← target_address                              │
│                                                             │
│  ALU Status Flags:                                        │
│  • Zero (Z): Result = 0                                   │
│  • Negative (N): Result < 0                               │
│  • Carry (C): Carry out from MSB                          │
│  • Overflow (V): Signed arithmetic overflow               │
│                                                             │
│  Effective Address Calculations:                           │
│  • Direct: EA = Address                                    │
│  • Indirect: EA = M[Address]                              │
│  • Displacement: EA = Register + Offset                   │
│  • Indexed: EA = Base + Index                             │
└─────────────────────────────────────────────────────────────┘
```

### Comparison Table: Hardwired vs Microprogrammed Control
```
┌─────────────────────────────────────────────────────────────┐
│           CONTROL UNIT COMPARISON                          │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  Aspect           │ Hardwired        │ Microprogrammed     │
│  ─────────────────┼──────────────────┼─────────────────────│
│  Speed            │ Very Fast        │ Slower              │
│  Flexibility      │ Fixed            │ Highly Flexible     │
│  Cost             │ Lower            │ Higher              │
│  Design Time      │ Longer           │ Shorter             │
│  Debugging        │ Difficult        │ Easier              │
│  Modification     │ Hardware change  │ Software change     │
│  Complexity       │ High for complex │ Lower logic         │
│                   │ instructions     │ complexity          │
│  Memory Required  │ None for control │ Control memory      │
│  Applications     │ RISC processors  │ CISC processors     │
│                   │ Simple CPUs      │ Complex CPUs        │
└─────────────────────────────────────────────────────────────┘
```

### Exam Preparation Tips
```
┌─────────────────────────────────────────────────────────────┐
│                  EXAM PREPARATION GUIDE                    │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  Important Topics for Exams:                              │
│  1. Basic computer structure and CPU organization          │
│  2. Register organization and addressing modes             │
│  3. Instruction formats and execution cycle                │
│  4. Stack operations and applications                      │
│  5. Control unit design (hardwired vs microprogrammed)     │
│  6. Microinstruction formats and sequencing                │
│  7. ALU operations and status flags                        │
│  8. Bus structure and I/O organization                     │
│  9. Program counter and register transfer language         │
│                                                             │
│  Practice Problems:                                        │
│  • Draw CPU block diagrams with all components             │
│  • Design instruction formats for different operations     │
│  • Trace instruction execution cycles step by step         │
│  • Convert between different addressing modes              │
│  • Design microprogram sequences for instructions          │
│  • Calculate effective addresses for various modes         │
│  • Analyze stack operations in detail                      │
│  • Compare hardwired vs microprogrammed approaches         │
│                                                             │
│  Study Strategy:                                           │
│  • Focus on understanding concepts over memorization       │
│  • Practice drawing diagrams from memory                   │
│  • Work through numerical examples and calculations        │
│  • Compare and contrast different design approaches        │
│  • Understand trade-offs in architectural decisions        │
│  • Review all ASCII diagrams and trace through examples    │
│                                                             │
│  Common Exam Question Types:                               │
│  • Block diagram drawing and labeling                      │
│  • Instruction format design and analysis                  │
│  • Address calculation for different modes                 │
│  • Control unit design comparison                          │
│  • Microprogram writing for given instructions             │
│  • Stack operation tracing                                 │
│  • Register transfer language notation                     │
│  • CPU performance calculations                            │
└─────────────────────────────────────────────────────────────┘
```

### Quick Review Checklist
```
┌─────────────────────────────────────────────────────────────┐
│                    FINAL CHECKLIST                         │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  □ Understand Von Neumann architecture components          │
│  □ Know CPU internal organization and register types       │
│  □ Memorize instruction formats (R, I, J types)            │
│  □ Practice all addressing mode calculations               │
│  □ Understand fetch-decode-execute cycle                   │
│  □ Know stack operations and applications                  │
│  □ Compare hardwired vs microprogrammed control            │
│  □ Understand microinstruction formats                     │
│  □ Know bus structure and characteristics                  │
│  □ Practice RTL notation and examples                      │
│  □ Understand ALU operations and status flags              │
│  □ Know I/O system organization                            │
│  □ Review all formulas and calculations                    │
│  □ Practice drawing diagrams from memory                   │
│  □ Understand design trade-offs and comparisons            │
└─────────────────────────────────────────────────────────────┘
```

---