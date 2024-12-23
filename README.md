# Multicycle RISC-V processor with support for ADDI and BNE instructions.

## Problem Statement
Design a 5 – stage (Instruction Fetch; Decode; Execute; Memory Access; Write Back) multi-cycle RISC processor that can execute following instructions.
0000 ADDI reg1, reg2, 20
0004 BNE reg3, reg4, 4
Initialize the register file with the following data reg2 = 4BFEA43 reg3 = 11AB0 reg4 = 11AB0

## Design

![image](https://github.com/user-attachments/assets/f7364919-7152-4142-bf72-10bf0a8db40b)

Notice that both of these instructions do not need to perform memory write and read, so we can remove the MDR and all control signals associated with it. Since we are not performing any jump instructions, we can get rid of some multiplexers and a Shift Left 2 block. We can also get rid of ALU control – the net Instruction [5:0] is useless since the immediate value is stored here – all information necessary can be gleaned from the opcode which is sent to the main Control unit. Taking all of this into consideration, the updated datapath is as shown below.

## Simulations

![image](https://github.com/user-attachments/assets/3d8bee90-6f6f-4566-b67a-06739cc24c53)

The output waveforms are as expected: ADDI should produce 4BFEA43 + 14 = 4BFEA57 and the BNE instruction will not branch since both the registers are equal, which is reflected in the program counter not changing. The program completes in seven cycles – 4 for the ADDI instruction and 3 for the BNE instruction.


