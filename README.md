# Fifo-Verification-using-System-verilog

This repository contains a simple **First-In First-Out (FIFO) buffer** designed in **SystemVerilog**.  
It demonstrates fundamental digital design principles such as memory management, read/write pointers, and handling **empty/full conditions**.

##  Key Features
 **Data Width**: 8-bit  
 **Depth**: 16 entries (configurable)  
 **Synchronous Operation**: Single clock domain  
 **Reset Support**: Active-high reset clears pointers & counter  
 **Status Flags**:
   `empty` → High when FIFO has no data  
   `full`  → High when FIFO is completely filled  

##  Module Description

### `FIFO`
| Port | Direction | Width | Description |
|------|-----------|-------|-------------|
| `clk`   | Input  | 1   | Clock signal |
| `rst`   | Input  | 1   | Active-high reset |
| `wr`    | Input  | 1   | Write enable |
| `rd`    | Input  | 1   | Read enable |
| `din`   | Input  | 8   | Data input |
| `dout`  | Output | 8   | Data output |
| `empty` | Output | 1   | FIFO empty flag |
| `full`  | Output | 1   | FIFO full flag |

**Internal Signals**
 `wptr` (write pointer): Tracks next memory location for write  
 `rptr` (read pointer): Tracks next memory location for read  
 `cnt`  : Counts stored elements (0–16)  
`mem[15:0]`: FIFO memory storage  

##  Operation

1. **Reset (`rst=1`)**
    Clears pointers (`wptr=0`, `rptr=0`)  
    Resets counter (`cnt=0`)  

2. **Write (`wr=1` and `full=0`)**
    Stores `din` into `mem[wptr]`  
    Increments `wptr` and `cnt`  

3. **Read (`rd=1` and `empty=0`)**
    Outputs `mem[rptr]` → `dout`  
    Increments `rptr`, decrements `cnt`  
