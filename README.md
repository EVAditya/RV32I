# Complete RV32I processor

An RV32I processor with single-cycle and pipelined implementation. 
# Opcodes implemented

Basically, every opcode in RV32I except  __ecall__ and __ebreak__ is implemented.
But I shall elaborate

## R-Type Instructions
| Opcode | Description                          |
|--------|--------------------------------------|
| ADD    | rd = rs1 + rs2                       |
| SUB    | rd = rs1 - rs2                       |
| SLL    | rd = rs1 << rs2[4:0]                 |
| SLT    | rd = (rs1 < rs2) ? 1 : 0 (signed)    |
| SLTU   | rd = (rs1 < rs2) ? 1 : 0 (unsigned)  |
| XOR    | rd = rs1 ^ rs2                       |
| SRL    | rd = rs1 >> rs2[4:0] (logical)       |
| SRA    | rd = rs1 >> rs2[4:0] (arithmetic)    |
| OR     | rd = rs1 \| rs2                      |
| AND    | rd = rs1 & rs2                       |

## Immediate Operations (I-Type)
| Opcode | Description                          |
|--------|--------------------------------------|
| ADDI   | rd = rs1 + imm[11:0]                 |
| SLTI   | rd = (rs1 < imm) ? 1 : 0 (signed)    |
| SLTIU  | rd = (rs1 < imm) ? 1 : 0 (unsigned)  |
| XORI   | rd = rs1 ^ imm[11:0]                 |
| ORI    | rd = rs1 \| imm[11:0]                |
| ANDI   | rd = rs1 & imm[11:0]                 |
| SLLI   | rd = rs1 << imm[4:0]                 |
| SRLI   | rd = rs1 >> imm[4:0] (logical)       |
| SRAI   | rd = rs1 >> imm[4:0] (arithmetic)    |

## Load Type Instructions (I-Type)
| Opcode | Description                          |
|--------|--------------------------------------|
| LB     | rd = SignExt(Mem[rs1 + imm][7:0])    |
| LH     | rd = SignExt(Mem[rs1 + imm][15:0])   |
| LW     | rd = SignExt(Mem[rs1 + imm][31:0])   |
| LBU    | rd = ZeroExt(Mem[rs1 + imm][7:0])    |
| LHU    | rd = ZeroExt(Mem[rs1 + imm][15:0])   |



## S-Type (Store Operations)
| Opcode | Description                          |
|--------|--------------------------------------|
| SB     | Mem[rs1 + imm] = rs2[7:0]            |
| SH     | Mem[rs1 + imm] = rs2[15:0]           |
| SW     | Mem[rs1 + imm] = rs2[31:0]           |

## B-Type (Branch Operations)
| Opcode | Description                          |
|--------|--------------------------------------|
| BEQ    | if (rs1 == rs2) pc += imm            |
| BNE    | if (rs1 != rs2) pc += imm            |
| BLT    | if (rs1 < rs2) pc += imm (signed)    |
| BGE    | if (rs1 >= rs2) pc += imm (signed)   |
| BLTU   | if (rs1 < rs2) pc += imm (unsigned)  |
| BGEU   | if (rs1 >= rs2) pc += imm (unsigned) |

## U-Type (Upper Immediate Operations)
| Opcode | Description                          |
|--------|--------------------------------------|
| LUI    | rd = imm << 12                        |
| AUIPC  | rd = pc + (imm << 12)                 |

## Jump Operations
| Opcode | Description                          | Type |
|--------|--------------------------------------| -----|
| JAL    | rd = pc + 4; pc += imm               |J-Type|
| JALR   | rd = pc + 4; pc = (rs1 + imm) & ~1   |I-Type|


# Innovative Approaches
 - Added a mux to select full words, half-words, and bytes to data memory and registers to load and store half-words and bytes.
 - Tweaked PC circuitry to include JALR instruction

 # Suggestions
 - You get standardised RISC V single cycle processor codes in verilog for various GitHub files. But I tweaked the code at several places to include other opcodes. So take this code with a pinch of salt. The code is correct, but may not be the most efficient or standard processor. But I did not find any standardised sources for RV332I processor so I can't help you there either :(. So adjust with this.
