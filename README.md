# ⚡ C16 — Compact 16 Instruction Set Architecture

**C16 — Compact 16 Instruction Set Architecture** is a minimal ISA with exactly **16 instructions**.  
It is designed to be **simple, easy to decode, and compiler‑friendly**, while still supporting **bare‑metal C programming**.  
The ISA uses a clean **4‑bit opcode space** (0000–1111).

---

## ✨ Instruction Categories

### 1. Memory Access
| Opcode | Binary | Mnemonic | Description |
|--------|--------|----------|-------------|
| 0x0    | 0000   | LDR R, [Rp+off] | Load from memory at register pointer + offset into R |
| 0x1    | 0001   | STR R, [Rp+off] | Store R into memory at register pointer + offset |

### 2. Data Movement
| Opcode | Binary | Mnemonic | Description |
|--------|--------|----------|-------------|
| 0x2    | 0010   | MOV R1, R2 | Copy register contents |
| 0x3    | 0011   | LDI R, #const | Load immediate constant into register |

### 3. Arithmetic
| Opcode | Binary | Mnemonic | Description |
|--------|--------|----------|-------------|
| 0x4    | 0100   | ADD R1, R2 | R1 = R1 + R2 (Flags updated) |
| 0x5    | 0101   | SUB R1, R2 | R1 = R1 - R2 (Flags updated) |

### 4. Logic
| Opcode | Binary | Mnemonic | Description |
|--------|--------|----------|-------------|
| 0x6    | 0110   | AND R1, R2 | Bitwise AND (Flags updated) |
| 0x7    | 0111   | OR R1, R2  | Bitwise OR (Flags updated) |
| 0x8    | 1000   | XOR R1, R2 | Bitwise XOR (Flags updated) |

### 5. Control Flow & System
| Opcode | Binary | Mnemonic | Description |
|--------|--------|----------|-------------|
| 0x9    | 1001   | JZ R | Jump or branch when previous operation is zero to address in register |
| 0xA    | 1010   | PUSH R      | Push register value into stack memory |
| 0xB    | 1011   | POP R       | Pop value from stack memory into register |
| 0xC    | 1100   | INP R, port | Read from I/O port into register |
| 0xD    | 1101   | OUT port, R | Write register value to I/O port |
| 0xE    | 1110   | TRAP #n     | Trap to fixed handler vector (system call/exception) |
| 0xF    | 1111   | RET         | Return from subroutine or trap (restore PC from stack/register) |

---

## 🏷️ Instruction Set (Binary Opcodes)

| Opcode (Binary) | Opcode (Hex) | Mnemonic        | Operands        | Description |
|-----------------|--------------|-----------------|-----------------|-------------|
| `0000`          | 0x0          | **LDR R, [Rp+off]** | R, Rp, offset | Load word from memory at register pointer Rp + offset into R |
| `0001`          | 0x1          | **STR R, [Rp+off]** | R, Rp, offset | Store word from R into memory at register pointer Rp + offset |
| `0010`          | 0x2          | **MOV R1, R2**  | R1, R2          | Copy register contents |
| `0011`          | 0x3          | **LDI R, #const** | R, const      | Load immediate constant into register |
| `0100`          | 0x4          | **ADD R1, R2**  | R1, R2          | Add registers (Flags updated) |
| `0101`          | 0x5          | **SUB R1, R2**  | R1, R2          | Subtract registers (Flags updated) |
| `0110`          | 0x6          | **AND R1, R2**  | R1, R2          | Bitwise AND (Flags updated) |
| `0111`          | 0x7          | **OR R1, R2**   | R1, R2          | Bitwise OR (Flags updated) |
| `1000`          | 0x8          | **XOR R1, R2**  | R1, R2          | Bitwise XOR (Flags updated) |
| `1001`          | 0x9          | **JZ, R**       | cond, R         | Jump or branch on condition to address in register |
| `1010`          | 0xA          | **PUSH R**      | R               | Push register value into stack memory |
| `1011`          | 0xB          | **POP R**       | R               | Pop value from stack memory into register |
| `1100`          | 0xC          | **INP R, port** | R, port         | Read from I/O port into register |
| `1101`          | 0xD          | **OUT port, R** | port, R         | Write register value to I/O port |
| `1110`          | 0xE          | **TRAP #n**     | n               | Trap to fixed handler vector (system call/exception) |
| `1111`          | 0xF          | **RET**         | —               | Return from subroutine or trap (restore PC from stack/register) |

---

## 📜 Encoding Notes
- **Opcode field**: 4 bits (selects one of 16 instructions)  
- **Register fields**: 6 bits each (up to 64 registers)  
- **Offset field**: included only in LDR/STR (for array/pointer arithmetic)  
- **Immediate/addr fields**: variable length depending on instruction format  
- **Instruction word size**: typically 16 bits for compactness  

---

## ✅ Purpose
C16 is designed as a **minimal yet complete ISA** for learning, experimentation, and bare‑metal C programming.  
Its simplicity makes it ideal for teaching computer architecture, building emulators, or experimenting with compiler backends.
