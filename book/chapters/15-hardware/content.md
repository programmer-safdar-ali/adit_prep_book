# Chapter 15: Computer Hardware & Architecture

## Overview

Understanding computer hardware and architecture is fundamental for IT professionals managing infrastructure, making procurement decisions, and troubleshooting system issues. For Assistant Directors IT in public service, this knowledge enables effective hardware lifecycle management, informed capacity planning, and optimal technology investments. This chapter covers computer organization from Von Neumann architecture to modern multi-core processors, memory hierarchy, storage technologies, motherboard components, and server hardware specifications.

## Learning Objectives

After completing this chapter, you will be able to:

- Explain Von Neumann and Harvard architectures and their implications
- Describe CPU components, instruction cycles, and modern processor features
- Understand the memory hierarchy from registers to secondary storage
- Differentiate between RAM, ROM, and various storage technologies
- Identify motherboard components and expansion interfaces
- Evaluate server hardware specifications for government IT procurement
- Apply performance metrics and troubleshooting techniques

---

## 15.1 Computer Organization

### Von Neumann Architecture

**Concept**: Single memory space stores both instructions and data.

**Architecture**:
```
┌─────────────────────────────────────────────────────┐
│                        CPU                          │
│  ┌─────────────┐    ┌───────────────────────────┐  │
│  │   Control   │◄──►│    Arithmetic Logic Unit  │  │
│  │    Unit     │    │         (ALU)             │  │
│  └──────┬──────┘    └───────────────────────────┘  │
│         │                        ▲                  │
│         │         ┌──────────────┴──────────────┐  │
│         └────────►│        Registers            │  │
│                   └──────────────┬──────────────┘  │
└──────────────────────────────────┼──────────────────┘
                                   │
                          ┌────────▼────────┐
                          │   System Bus    │
                          │ (Address, Data, │
                          │   Control)      │
                          └────────┬────────┘
                                   │
                          ┌────────▼────────┐
                          │     Memory      │
                          │ (Instructions   │
                          │   & Data)       │
                          └─────────────────┘
```

**Characteristics**:
- Single memory for code and data
- Sequential instruction execution
- Bottleneck: memory access (Von Neumann bottleneck)
- Simple design, widely used

**Key Components**:
| Component | Function |
|-----------|----------|
| Control Unit | Fetches and decodes instructions |
| ALU | Performs arithmetic and logical operations |
| Registers | Fast temporary storage |
| Memory | Stores programs and data |
| I/O | Interface to external devices |

### Harvard Architecture

**Concept**: Separate memory spaces for instructions and data.

**Architecture**:
```
                         ┌──────────┐
                         │   CPU    │
                         └────┬─────┘
                              │
              ┌───────────────┼───────────────┐
              │               │               │
       ┌──────▼──────┐  ┌─────▼─────┐  ┌──────▼──────┐
       │ Instruction │  │   Data    │  │    I/O     │
       │   Memory    │  │  Memory   │  │  Interface │
       └─────────────┘  └───────────┘  └────────────┘
```

**Advantages**:
- Simultaneous instruction and data access
- Higher performance
- Better security (code/data separation)

**Use Cases**:
- Digital Signal Processors (DSP)
- Microcontrollers
- Modern CPU cache (modified Harvard)

### Stored Program Concept

**Principle**: Programs are stored in memory alongside data.

**Benefits**:
- Programs can be modified during execution
- Universal machine concept
- Software flexibility

---

## 15.2 CPU Architecture

### CPU Components

#### Arithmetic Logic Unit (ALU)

**Functions**:
- Arithmetic operations: addition, subtraction, multiplication, division
- Logical operations: AND, OR, NOT, XOR
- Comparison operations: equal, greater than, less than
- Bit manipulation: shift, rotate

#### Control Unit

**Functions**:
- Fetch instructions from memory
- Decode instructions
- Generate control signals
- Coordinate data movement

#### Registers

**Types**:
| Register | Purpose |
|----------|---------|
| Program Counter (PC) | Address of next instruction |
| Instruction Register (IR) | Current instruction |
| Accumulator (ACC) | ALU results |
| Stack Pointer (SP) | Top of stack address |
| General Purpose | Data manipulation |
| Status/Flag Register | Condition codes |

### Instruction Cycle

**Fetch-Decode-Execute Cycle**:
```
┌────────┐     ┌────────┐     ┌────────┐     ┌────────┐
│ FETCH  │────►│ DECODE │────►│EXECUTE │────►│ STORE  │
│        │     │        │     │        │     │        │
│Read    │     │Interpret│    │Perform │     │Write   │
│inst    │     │opcode   │    │operation│    │result  │
└────────┘     └────────┘     └────────┘     └────────┘
     ▲                                            │
     └────────────────────────────────────────────┘
```

**Detailed Steps**:
1. **Fetch**: Read instruction from memory at PC address
2. **Decode**: Interpret instruction opcode
3. **Execute**: Perform the operation
4. **Store**: Write results (if needed)
5. **Increment PC**: Move to next instruction

### Pipelining

**Concept**: Overlapping instruction execution stages.

**5-Stage Pipeline**:
```
Time →    1    2    3    4    5    6    7    8
Inst 1   [IF] [ID] [EX] [MEM][WB]
Inst 2        [IF] [ID] [EX] [MEM][WB]
Inst 3             [IF] [ID] [EX] [MEM][WB]
Inst 4                  [IF] [ID] [EX] [MEM][WB]

IF = Instruction Fetch
ID = Instruction Decode
EX = Execute
MEM = Memory Access
WB = Write Back
```

**Pipeline Hazards**:
| Hazard Type | Description | Solution |
|-------------|-------------|----------|
| Structural | Resource conflict | More hardware |
| Data | Dependency on previous result | Forwarding, stalls |
| Control | Branch uncertainty | Branch prediction |

### Superscalar Architecture

**Concept**: Multiple execution units for parallel instruction execution.

**Features**:
- Multiple ALUs
- Out-of-order execution
- Speculative execution
- Multiple pipelines

### CISC vs. RISC

| Feature | CISC | RISC |
|---------|------|------|
| Instructions | Complex, variable length | Simple, fixed length |
| Addressing Modes | Many | Few |
| Registers | Fewer | Many |
| Cycles/Instruction | Multiple | Usually one |
| Examples | x86, x64 | ARM, MIPS, RISC-V |

### Processor Specifications

| Specification | Description | Typical Values |
|---------------|-------------|----------------|
| Clock Speed | Cycles per second | 2.0 - 5.0 GHz |
| Cores | Processing units | 4 - 64+ cores |
| Threads | Simultaneous threads | 2 per core (SMT) |
| Cache | Fast memory | L1: 64KB, L2: 512KB, L3: 8MB+ |
| TDP | Thermal design power | 35W - 250W |
| Architecture | Instruction set | x86-64, ARM64 |

---

## 15.3 Memory Hierarchy

### Memory Levels

```
                    ┌───────────┐
        Faster      │ Registers │      Smaller
        More        ├───────────┤      More
        Expensive   │  L1 Cache │      Expensive
                    ├───────────┤
                    │  L2 Cache │
                    ├───────────┤
                    │  L3 Cache │
                    ├───────────┤
                    │ Main RAM  │
                    ├───────────┤
        Slower      │   SSD     │      Larger
        Cheaper     ├───────────┤      Cheaper
                    │   HDD     │
                    ├───────────┤
                    │   Tape    │
                    └───────────┘
```

### Cache Memory

**Purpose**: Bridge speed gap between CPU and main memory.

**Cache Levels**:
| Level | Location | Size | Speed |
|-------|----------|------|-------|
| L1 | Per core | 32-64 KB | 4 cycles |
| L2 | Per core | 256-512 KB | 12 cycles |
| L3 | Shared | 4-64 MB | 40 cycles |

**Cache Concepts**:
- **Cache Hit**: Data found in cache
- **Cache Miss**: Data not in cache, fetch from lower level
- **Hit Rate**: Percentage of accesses found in cache
- **Write-Through**: Write to cache and memory
- **Write-Back**: Write to cache, update memory later

**Cache Mapping**:
| Method | Description | Trade-off |
|--------|-------------|-----------|
| Direct Mapped | Each block maps to one line | Simple, conflicts |
| Fully Associative | Block can go anywhere | Flexible, complex |
| Set Associative | Compromise (N-way) | Balanced |

### Virtual Memory

**Concept**: Use disk as extension of RAM.

**Components**:
- **Page**: Fixed-size memory block (typically 4KB)
- **Page Table**: Maps virtual to physical addresses
- **TLB**: Translation Lookaside Buffer (cache for page table)

**Address Translation**:
```
Virtual Address          Physical Address
┌──────────┬─────────┐   ┌──────────┬─────────┐
│ Page No. │ Offset  │ → │ Frame No.│ Offset  │
└──────────┴─────────┘   └──────────┴─────────┘
              ▲
              │
        Page Table
```

---

## 15.4 RAM Types

### DRAM (Dynamic RAM)

**Characteristics**:
- Uses capacitors (requires refresh)
- Slower than SRAM
- Less expensive
- Used for main memory

**Types**:
| Type | Features | Data Rate |
|------|----------|-----------|
| SDRAM | Synchronous, clock-aligned | 133 MHz |
| DDR | Double Data Rate | 200-400 MT/s |
| DDR2 | Faster, lower voltage | 400-1066 MT/s |
| DDR3 | Further improvements | 800-2133 MT/s |
| DDR4 | Higher density, lower power | 1600-3200 MT/s |
| DDR5 | Latest, highest bandwidth | 3200-8400 MT/s |

**DDR Comparison**:
| Feature | DDR3 | DDR4 | DDR5 |
|---------|------|------|------|
| Voltage | 1.5V | 1.2V | 1.1V |
| Pins | 240 | 288 | 288 |
| Max Capacity | 8GB/DIMM | 64GB/DIMM | 512GB/DIMM |
| Prefetch | 8n | 8n | 16n |

### SRAM (Static RAM)

**Characteristics**:
- Uses flip-flops (no refresh needed)
- Very fast
- More expensive
- Used for cache

### ECC RAM

**Error Correcting Code Memory**:
- Detects and corrects single-bit errors
- Detects double-bit errors
- Required for servers
- Adds ~12.5% overhead (72 bits vs. 64 bits)

---

## 15.5 ROM Types

| Type | Full Name | Programmable | Erasable |
|------|-----------|--------------|----------|
| ROM | Read-Only Memory | Factory only | No |
| PROM | Programmable ROM | Once | No |
| EPROM | Erasable PROM | Multiple | UV light |
| EEPROM | Electrically Erasable PROM | Multiple | Electrical |
| Flash | Flash Memory | Multiple | Block erase |

**Flash Memory Applications**:
- USB drives
- SSD storage
- BIOS/UEFI firmware
- Memory cards

---

## 15.6 Storage Devices

### Hard Disk Drive (HDD)

**Components**:
```
          ┌─────────────────────────┐
          │        Platters         │
          │    ┌───────────────┐    │
          │    │ ╭───────────╮ │    │
          │    │ │  ○  ○  ○  │ │    │  ← Tracks
          │    │ │           │ │    │
          │    │ │  ○  ○  ○  │ │    │
          │    │ ╰───────────╯ │    │
          │    └───────────────┘    │
          │         Spindle ────────┤
          │    ┌─────────────────┐  │
          │    │  Read/Write    │  │  ← Actuator Arm
          │    │     Head       │  │
          │    └─────────────────┘  │
          └─────────────────────────┘
```

**Specifications**:
| Parameter | Values | Impact |
|-----------|--------|--------|
| RPM | 5400/7200/10K/15K | Higher = faster access |
| Cache | 8-256 MB | Improves performance |
| Form Factor | 3.5", 2.5" | Size/capacity |
| Interface | SATA, SAS | Speed, reliability |

**Performance Metrics**:
- **Seek Time**: Time to move head to track (8-15 ms)
- **Rotational Latency**: Time for sector to rotate (4-8 ms)
- **Transfer Rate**: Data speed (100-250 MB/s)

### Solid State Drive (SSD)

**NAND Flash Types**:
| Type | Bits/Cell | Endurance | Speed | Cost |
|------|-----------|-----------|-------|------|
| SLC | 1 | 100,000 P/E | Fastest | $$$$ |
| MLC | 2 | 10,000 P/E | Fast | $$$ |
| TLC | 3 | 3,000 P/E | Good | $$ |
| QLC | 4 | 1,000 P/E | Slower | $ |

**SSD Interfaces**:
| Interface | Speed | Form Factor |
|-----------|-------|-------------|
| SATA | 600 MB/s | 2.5" |
| NVMe (PCIe 3.0 x4) | 3,500 MB/s | M.2 |
| NVMe (PCIe 4.0 x4) | 7,000 MB/s | M.2 |
| NVMe (PCIe 5.0 x4) | 14,000 MB/s | M.2 |

**SSD Maintenance**:
- **TRIM**: Informs SSD of deleted blocks
- **Wear Leveling**: Distributes writes evenly
- **Over-provisioning**: Reserved capacity for GC

### HDD vs. SSD Comparison

| Feature | HDD | SSD |
|---------|-----|-----|
| Speed | Slower | Faster |
| Durability | Moving parts | No moving parts |
| Power | Higher | Lower |
| Noise | Audible | Silent |
| Cost/GB | Lower | Higher |
| Capacity | Up to 20+ TB | Up to 8+ TB |
| Best For | Bulk storage | Performance |

---

## 15.7 Motherboard Components

### Motherboard Layout

```
┌─────────────────────────────────────────────────────────┐
│  ┌─────────┐  ┌──────────────┐  ┌───────────────────┐  │
│  │ CPU     │  │ RAM Slots    │  │ Power Connectors  │  │
│  │ Socket  │  │ ════════════ │  │ 24-pin ATX       │  │
│  │         │  │ ════════════ │  │ 8-pin CPU        │  │
│  └─────────┘  │ ════════════ │  └───────────────────┘  │
│               │ ════════════ │                          │
│  ┌─────────┐  └──────────────┘  ┌───────────────────┐  │
│  │Chipset  │                    │ M.2 Slots         │  │
│  │         │  ┌──────────────┐  │ ─────────────────  │  │
│  └─────────┘  │ PCIe x16     │  │ ─────────────────  │  │
│               │ ══════════════│  └───────────────────┘  │
│               │ PCIe x1      │                          │
│  ┌─────────┐  │ ═════════    │  ┌───────────────────┐  │
│  │BIOS/    │  │ PCIe x16     │  │ SATA Ports        │  │
│  │UEFI     │  │ ══════════════│  │ ▫ ▫ ▫ ▫ ▫ ▫     │  │
│  │Chip     │  └──────────────┘  └───────────────────┘  │
│  └─────────┘                                            │
│  ┌────────────────────────────────────────────────────┐│
│  │ I/O Panel: USB, Audio, Ethernet, Display Outputs   ││
│  └────────────────────────────────────────────────────┘│
└─────────────────────────────────────────────────────────┘
```

### Chipset

**Function**: Manages data flow between CPU, memory, and peripherals.

**Modern Architecture**:
- **Platform Controller Hub (PCH)**: Single chip handling I/O
- Connected to CPU via DMI (Direct Media Interface)

### BIOS vs. UEFI

| Feature | BIOS | UEFI |
|---------|------|------|
| Interface | Text-based | Graphical |
| Boot Partition | MBR (2TB limit) | GPT (9.4ZB limit) |
| Boot Speed | Slower | Faster |
| Secure Boot | No | Yes |
| Driver Location | ROM | EFI partition |

### Expansion Slots

**PCIe (PCI Express)**:
| Version | x1 Bandwidth | x16 Bandwidth |
|---------|--------------|---------------|
| PCIe 3.0 | 1 GB/s | 16 GB/s |
| PCIe 4.0 | 2 GB/s | 32 GB/s |
| PCIe 5.0 | 4 GB/s | 64 GB/s |

**Slot Sizes**:
- x1: Sound cards, USB expansion
- x4: NVMe SSDs, RAID controllers
- x8: Network cards, storage controllers
- x16: Graphics cards, compute accelerators

### RAM Slots

**DIMM Types**:
| Type | Form Factor | Use |
|------|-------------|-----|
| UDIMM | Desktop | Consumer PCs |
| RDIMM | Server | Registered, larger capacity |
| LRDIMM | Server | Load-reduced, highest capacity |
| SO-DIMM | Laptop | Small form factor |

### Storage Interfaces

| Interface | Speed | Cable | Hot-Swap |
|-----------|-------|-------|----------|
| SATA III | 6 Gb/s | Data + Power | Yes |
| SAS | 12 Gb/s | Single | Yes |
| M.2 (SATA) | 6 Gb/s | On-board | No |
| M.2 (NVMe) | 32+ Gb/s | On-board | No |
| U.2 | 32 Gb/s | Cable | Yes |

---

## 15.8 Bus Architecture

### Bus Types

| Bus | Function | Width |
|-----|----------|-------|
| Address Bus | Memory location | 32-64 bits |
| Data Bus | Data transfer | 32-64 bits |
| Control Bus | Control signals | Multiple lines |

### Front Side Bus vs. Modern

**Legacy (FSB)**:
```
CPU ←─── FSB ───→ Northbridge ←─── Memory Bus ───→ RAM
                      │
                  Southbridge ←─── I/O Devices
```

**Modern (Direct)**:
```
CPU ←─── Direct ───→ RAM
 │
 └─── DMI ───→ PCH ←─── I/O Devices
```

---

## 15.9 Peripheral Interfaces

### USB (Universal Serial Bus)

| Version | Speed | Connector |
|---------|-------|-----------|
| USB 2.0 | 480 Mbps | Type-A, Mini, Micro |
| USB 3.0 | 5 Gbps | Type-A (blue), Type-C |
| USB 3.1 | 10 Gbps | Type-A, Type-C |
| USB 3.2 | 20 Gbps | Type-C |
| USB4 | 40 Gbps | Type-C |

### Display Interfaces

| Interface | Resolution | Features |
|-----------|------------|----------|
| VGA | 1920×1080 | Analog, legacy |
| DVI | 2560×1600 | Digital/analog |
| HDMI 2.1 | 10K | Audio, ARC |
| DisplayPort 2.0 | 16K | Daisy-chain |

### Thunderbolt

| Version | Speed | Connectors |
|---------|-------|------------|
| Thunderbolt 3 | 40 Gbps | USB-C |
| Thunderbolt 4 | 40 Gbps | USB-C (certified) |
| Thunderbolt 5 | 80 Gbps | USB-C |

---

## 15.10 Power Supply

### Power Specifications

**Form Factors**:
- ATX: Standard desktop
- SFX: Small form factor
- TFX: Thin form factor

**Efficiency Ratings (80 Plus)**:
| Rating | 20% Load | 50% Load | 100% Load |
|--------|----------|----------|-----------|
| 80 Plus | 80% | 80% | 80% |
| Bronze | 82% | 85% | 82% |
| Silver | 85% | 88% | 85% |
| Gold | 87% | 90% | 87% |
| Platinum | 90% | 92% | 89% |
| Titanium | 92% | 94% | 90% |

**Power Connectors**:
| Connector | Pins | Purpose |
|-----------|------|---------|
| ATX Main | 24-pin | Motherboard power |
| EPS/CPU | 4/8-pin | CPU power |
| PCIe | 6/8-pin | Graphics card |
| SATA | 15-pin | Storage drives |
| Molex | 4-pin | Legacy devices |

---

## 15.11 Cooling Systems

### Air Cooling

**Components**:
- Heat sink: Absorbs heat from CPU
- Thermal paste: Fills gaps
- Fans: Move air across heat sink

**Fan Specifications**:
| Parameter | Common Values |
|-----------|---------------|
| Size | 80mm, 120mm, 140mm |
| Speed | 500-2000 RPM |
| Airflow | CFM (Cubic Feet/Minute) |
| Noise | dBA (decibels) |

### Liquid Cooling

**Types**:
- **AIO (All-In-One)**: Closed-loop, maintenance-free
- **Custom Loop**: Higher performance, requires maintenance

**Components**:
- Water block: Contacts CPU
- Radiator: Dissipates heat
- Pump: Circulates coolant
- Reservoir: Holds coolant

---

## 15.12 Server Hardware

### Server Types

| Type | Description | Use Case |
|------|-------------|----------|
| Tower | Standalone unit | Small office |
| Rack | 1U-4U rackmount | Data center |
| Blade | Modular in chassis | High density |

### Server Features

**Redundancy**:
- Redundant power supplies
- Hot-swap fans
- RAID storage
- Dual network interfaces

**Management**:
| Technology | Vendor |
|------------|--------|
| IPMI | Standard |
| iLO | HPE |
| iDRAC | Dell |
| IMM | Lenovo |

**Out-of-Band Management Features**:
- Remote power control
- Console access
- Hardware monitoring
- Firmware updates

---

## 15.13 Computer Generations

| Generation | Technology | Period | Examples |
|------------|------------|--------|----------|
| 1st | Vacuum tubes | 1940s-1950s | ENIAC, UNIVAC |
| 2nd | Transistors | 1950s-1960s | IBM 1401 |
| 3rd | Integrated Circuits | 1960s-1970s | IBM 360 |
| 4th | Microprocessors | 1970s-Present | Personal computers |
| 5th | AI/Quantum | Emerging | Quantum computers |

---

## 15.14 Performance Metrics

### CPU Performance

| Metric | Description |
|--------|-------------|
| MIPS | Million Instructions Per Second |
| FLOPS | Floating Point Operations Per Second |
| IPC | Instructions Per Clock |
| Clock Speed | GHz |

### Performance Laws

**Moore's Law**: Transistor count doubles every ~2 years.

**Amdahl's Law**:
```
Speedup = 1 / ((1 - P) + P/S)

P = Parallelizable portion
S = Speedup factor
```

**Example**:
```
If 90% is parallelizable and speedup is 10x:
Speedup = 1 / ((1 - 0.9) + 0.9/10)
        = 1 / (0.1 + 0.09)
        = 1 / 0.19
        = 5.26x maximum speedup
```

---

## 15.15 Hardware Troubleshooting

### POST (Power-On Self-Test)

**POST Process**:
1. Power good signal
2. CPU check
3. BIOS/UEFI initialization
4. Memory test
5. Peripheral detection
6. Boot device search

### Beep Codes (Example - AMI BIOS)

| Beeps | Meaning |
|-------|---------|
| 1 short | Normal POST |
| 1 long, 2 short | Video error |
| Continuous | RAM error |
| 3 short | Base memory error |
| 5 short | CPU error |

### Diagnostic Tools

| Tool | Purpose |
|------|---------|
| Memtest86 | Memory testing |
| CrystalDiskInfo | Drive health |
| HWiNFO | System information |
| CPU-Z | Processor details |
| Prime95 | CPU stress test |
| FurMark | GPU stress test |

---

## Hands-On Labs

### Lab 15.1: Memory Calculation

**Scenario**: Calculate memory requirements for a server.

**Requirements**:
- Operating System: 2GB
- Database: 32GB buffer pool
- Application: 8GB
- Reserve: 20% for OS overhead

**Calculation**:
```
Base requirement: 2 + 32 + 8 = 42GB
With 20% overhead: 42 × 1.2 = 50.4GB
Recommendation: 64GB (next power of 2)
```

### Lab 15.2: Power Supply Sizing

**Scenario**: Calculate PSU requirements.

**Components**:
| Component | TDP |
|-----------|-----|
| CPU (Intel i9) | 125W |
| GPU (RTX 3080) | 320W |
| RAM (4×16GB) | 20W |
| Storage (2 SSD) | 15W |
| Fans/Other | 30W |

**Calculation**:
```
Total: 125 + 320 + 20 + 15 + 30 = 510W
With 20% headroom: 510 × 1.2 = 612W
Recommendation: 750W PSU (80+ Gold)
```

### Lab 15.3: RAID Performance Analysis

**Scenario**: Compare RAID configurations for database server.

| RAID | Capacity (8×4TB) | Read Performance | Write Performance | Fault Tolerance |
|------|------------------|------------------|-------------------|-----------------|
| RAID 0 | 32TB | Excellent | Excellent | None |
| RAID 5 | 28TB | Good | Good | 1 drive |
| RAID 6 | 24TB | Good | Fair | 2 drives |
| RAID 10 | 16TB | Excellent | Good | 1/mirror |

**Recommendation**: RAID 10 for database (balance of performance and redundancy).

---

## Chapter Summary

- **Von Neumann Architecture**: Single memory for instructions and data, foundational to most computers
- **CPU Components**: ALU performs calculations, Control Unit manages execution, Registers provide fast storage
- **Instruction Cycle**: Fetch → Decode → Execute → Store
- **Pipelining**: Overlaps instruction stages for improved throughput
- **Memory Hierarchy**: Registers → Cache → RAM → SSD → HDD (speed vs. capacity trade-off)
- **Cache**: L1/L2/L3 bridge CPU-memory speed gap
- **DDR Evolution**: DDR3 → DDR4 → DDR5 with increasing speed and efficiency
- **Storage**: HDD for capacity, SSD for performance (NVMe faster than SATA)
- **Motherboard**: CPU socket, RAM slots, PCIe expansion, chipset manages I/O
- **Server Hardware**: Redundancy features (PSU, storage, network) and remote management

---

## Multiple Choice Questions

### Beginner Level

1. In Von Neumann architecture, where are both instructions and data stored?
   - A) Separate memories
   - B) Same memory
   - C) Only registers
   - D) External storage

   **Answer: B**
   *Explanation: Von Neumann architecture uses a single memory space for both instructions and data.*

2. What does the ALU perform?
   - A) Fetch instructions
   - B) Store data
   - C) Arithmetic and logical operations
   - D) Memory management

   **Answer: C**
   *Explanation: The Arithmetic Logic Unit performs arithmetic and logical operations.*

3. Which memory type is fastest?
   - A) Hard disk
   - B) RAM
   - C) Cache
   - D) Registers

   **Answer: D**
   *Explanation: Registers are the fastest memory, located within the CPU.*

4. DDR5 RAM uses lower voltage than DDR4. What is DDR5's voltage?
   - A) 1.5V
   - B) 1.35V
   - C) 1.2V
   - D) 1.1V

   **Answer: D**
   *Explanation: DDR5 operates at 1.1V, lower than DDR4's 1.2V.*

5. What does POST stand for?
   - A) Power Output System Test
   - B) Power-On Self-Test
   - C) Processor Operational Status Test
   - D) Peripheral Operating System Test

   **Answer: B**
   *Explanation: POST (Power-On Self-Test) is the hardware check that runs when a computer starts.*

### Intermediate Level

6. Which SSD interface provides the highest speed?
   - A) SATA
   - B) NVMe PCIe 4.0
   - C) USB 3.0
   - D) SAS

   **Answer: B**
   *Explanation: NVMe over PCIe 4.0 provides up to 7,000 MB/s, far exceeding SATA's 600 MB/s.*

7. What is the purpose of cache memory?
   - A) Long-term storage
   - B) Bridge the speed gap between CPU and RAM
   - C) Boot the operating system
   - D) Store BIOS settings

   **Answer: B**
   *Explanation: Cache provides fast temporary storage to reduce the speed difference between CPU and main memory.*

8. ECC memory is primarily used in:
   - A) Gaming PCs
   - B) Laptops
   - C) Servers
   - D) Tablets

   **Answer: C**
   *Explanation: ECC (Error Correcting Code) memory is used in servers for reliability and data integrity.*

9. Which NAND flash type has the highest endurance?
   - A) QLC
   - B) TLC
   - C) MLC
   - D) SLC

   **Answer: D**
   *Explanation: SLC (Single Level Cell) has the highest endurance at ~100,000 P/E cycles.*

10. UEFI replaced BIOS. Which feature does UEFI provide that BIOS doesn't?
    - A) Boot capability
    - B) Secure Boot
    - C) Keyboard support
    - D) Display output

    **Answer: B**
    *Explanation: UEFI introduced Secure Boot to prevent unauthorized bootloaders from running.*

### Advanced Level

11. According to Amdahl's Law, if 80% of a program is parallelizable with 4x speedup, the theoretical maximum speedup is:
    - A) 2.5x
    - B) 3.2x
    - C) 4.0x
    - D) 5.0x

    **Answer: A**
    *Explanation: Speedup = 1/((1-0.8) + 0.8/4) = 1/(0.2 + 0.2) = 1/0.4 = 2.5x*

12. In pipelining, a data hazard occurs when:
    - A) Two instructions need the same resource
    - B) An instruction depends on the result of a previous instruction
    - C) A branch instruction is encountered
    - D) Cache miss occurs

    **Answer: B**
    *Explanation: Data hazards occur when an instruction depends on the result of a prior instruction still in the pipeline.*

13. What is the main advantage of DDR memory over SDR?
    - A) Higher voltage
    - B) Data transfer on both clock edges
    - C) Larger capacity
    - D) Lower latency

    **Answer: B**
    *Explanation: DDR (Double Data Rate) transfers data on both rising and falling clock edges, doubling throughput.*

14. Which motherboard component manages data flow between CPU and peripherals?
    - A) CPU
    - B) RAM
    - C) Chipset/PCH
    - D) BIOS

    **Answer: C**
    *Explanation: The Platform Controller Hub (PCH) / Chipset manages data flow between CPU, memory, and I/O devices.*

15. PCIe 4.0 x16 provides how much bandwidth?
    - A) 16 GB/s
    - B) 32 GB/s
    - C) 64 GB/s
    - D) 128 GB/s

    **Answer: B**
    *Explanation: PCIe 4.0 provides 2 GB/s per lane, so x16 = 32 GB/s.*

16. Which technology allows servers to be managed even when powered off?
    - A) RAID
    - B) IPMI/iLO/iDRAC
    - C) ECC RAM
    - D) Hot-swap

    **Answer: B**
    *Explanation: IPMI, iLO, and iDRAC provide out-of-band management including remote power control.*

17. What does TDP indicate for a processor?
    - A) Maximum clock speed
    - B) Thermal design power (heat output)
    - C) Total data processed
    - D) Thread count

    **Answer: B**
    *Explanation: TDP (Thermal Design Power) indicates the heat a processor generates under load, used for cooling design.*

18. Harvard architecture's main advantage over Von Neumann is:
    - A) Lower cost
    - B) Simultaneous instruction and data access
    - C) Simpler design
    - D) Less memory required

    **Answer: B**
    *Explanation: Harvard architecture's separate memories allow simultaneous access to instructions and data.*

19. Which power supply efficiency rating requires 92% efficiency at 50% load?
    - A) 80 Plus Bronze
    - B) 80 Plus Gold
    - C) 80 Plus Platinum
    - D) 80 Plus Titanium

    **Answer: C**
    *Explanation: 80 Plus Platinum requires 92% efficiency at 50% load.*

20. In a 5-stage pipeline, how many instructions can be in progress simultaneously (ideal conditions)?
    - A) 1
    - B) 3
    - C) 5
    - D) 10

    **Answer: C**
    *Explanation: A 5-stage pipeline can have 5 instructions in different stages simultaneously.*

---

## References and Further Reading

1. "Computer Organization and Design" by Patterson and Hennessy
2. "Computer Architecture: A Quantitative Approach" by Hennessy and Patterson
3. Intel Developer Documentation - www.intel.com/developer
4. AMD Technical Documentation - www.amd.com/en/support/tech-docs
5. JEDEC Standards - www.jedec.org
6. Tom's Hardware - www.tomshardware.com
7. AnandTech - www.anandtech.com

---

*Chapter 15 completed. Understanding computer hardware and architecture enables IT leaders to make informed decisions about infrastructure investments and system design.*
