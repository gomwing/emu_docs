  PC-Engine Documenation: The HuC6280 CPU 

The HuC6280 CPU
===============

The PC-Engine uses a special version of the well-known 6502 CPU. It has additional Opcodes, more addressing-modes and a memory management unit (MMU). This is a list of Opcodes, that are available with the Hu6502 CPU.

Add With Carry (ADC)
--------------------

_Function_ Add the data located at the effective address specified by the operand to the contents of the accumulator. Add one to the result if the carry flag is set, and store the final result in the accumulator. This opcode takes one extra cycle to complete if the decimal mode flag D is set.

_Adressing Modes & Opcodes_

| Addressing Mode | Syntax | Opcode | \# of bytes | \# of cycles |
| --- | --- | --- | --- | --- |
| Immediate | ADC #nn | 69 nn | 2   | 2   |
| Zero Page | ADC ZZ | 65 ZZ | 2   | 4   |
| Zero Page, X | ADC ZZ, X | 75 ZZ | 2   | 4   |
| Indirect | ADC (ZZ) | 72 ZZ | 2   | 7   |
| Indexed Indirect, X | ADC (ZZ, X) | 61 ZZ | 2   | 7   |
| Indirect Indexed, Y | ADC (ZZ), Y | 71 ZZ | 2   | 7   |
| Absolute | ADC hhll | 6D ll hh | 3   | 5   |
| Absolute, X | ADC hhll, X | 7D ll hh | 3   | 5   |
| Absolute, Y | ADC hhll, Y | 79 ll hh | 3   | 5   |

_Flags Affected_

| N   | V   | T   | B   | D   | I   | Z   | C   |
| --- | --- | --- | --- | --- | --- | --- | --- |
| N   | V   | 0   | -   | -   | -   | Z   | C   |

And Accumulator with Memory (AND)
---------------------------------

_Function_ Bitwise logical AND the data located at the effective address specified by the operand with the contents of the accumulator. Each bit in the accumulator is ANDed with the corresponding bit in memory, with the result being stored in the respective accumulator bit.

_Adressing Modes & Opcodes_

| Addressing Mode | Syntax | Opcode | \# of bytes | \# of cycles |
| --- | --- | --- | --- | --- |
| Immediate | AND #nn | 29 nn | 2   | 2   |
| Zero Page | AND ZZ | 25 ZZ | 2   | 4   |
| Zero Page, X | AND ZZ, X | 35 ZZ | 2   | 4   |
| Indirect | AND (ZZ) | 32 ZZ | 2   | 7   |
| Indexed Indirect, X | AND (ZZ, X) | 21 ZZ | 2   | 7   |
| Indirect Indexed, Y | AND (ZZ), Y | 31 ZZ | 2   | 7   |
| Absolute | AND hhll | 2D ll hh | 3   | 5   |
| Absolute, X | AND hhll, X | 3D ll hh | 3   | 5   |
| Absolute, Y | AND hhll, Y | 39 ll hh | 3   | 5   |

_Flags Affected_

| N   | V   | T   | B   | D   | I   | Z   | C   |
| --- | --- | --- | --- | --- | --- | --- | --- |
| N   | -   | 0   | -   | -   | -   | Z   | -   |

Shift Memory or Accumulator Left (ASL)
--------------------------------------

_Function_ Shift the contents of the location specified by the operand left one bit. That is, bit one takes on the value originally found in bit zero, bit two takes the value originally in bit one, and so on; bit 7 is transferred into the carry flag; bit 0 is cleared. The arithmetic result of the operation is an unsigned multiplication by two.

_Adressing Modes & Opcodes_

| Addressing Mode | Syntax | Opcode | \# of bytes | \# of cycles |
| --- | --- | --- | --- | --- |
| Zero Page | ASL ZZ | 06 ZZ | 2   | 6   |
| Zero Page, X | ASL ZZ, X | 16 ZZ | 2   | 6   |
| Absolute | ASL hhll | 0E ll hh | 3   | 7   |
| Absolute, X | ASL hhll, X | 1E ll hh | 3   | 7   |
| Accumulator | ASL A | 0A  | 1   | 2   |

_Flags Affected_

| N   | V   | T   | B   | D   | I   | Z   | C   |
| --- | --- | --- | --- | --- | --- | --- | --- |
| N   | -   | 0   | -   | -   | -   | Z   | C   |

Branch on Bit Reset (BBRi)
--------------------------

_Function_ The _i_ th bit value in zero page memory location ZZ is tested. If it is clear, a branch is taken; if it is set, the instruction immediately following the three-byte BBRi instruction is executed. If the branch is taken, a one-byte signed displacement, fetched from the third byte of the instruction, is added to the program counter. Once the branch address has been calculated, the result is loaded into the program counter, transferring control to that location. The allowable range of the displacement is -128 to +127 _from the instruction immediately following the branch_ .

_Adressing Modes & Opcodes_

| Addressing Mode | Syntax | Opcode | \# of bytes | \# of cycles |
| --- | --- | --- | --- | --- |
| Zero Page, Relative | BBR0 ZZ, hhll | 0F ZZ rr | 3   | 6   |
| Zero Page, Relative | BBR1 ZZ, hhll | 1F ZZ rr | 3   | 6   |
| Zero Page, Relative | BBR2 ZZ, hhll | 2F ZZ rr | 3   | 6   |
| Zero Page, Relative | BBR3 ZZ, hhll | 3F ZZ rr | 3   | 6   |
| Zero Page, Relative | BBR4 ZZ, hhll | 4F ZZ rr | 3   | 6   |
| Zero Page, Relative | BBR5 ZZ, hhll | 5F ZZ rr | 3   | 6   |
| Zero Page, Relative | BBR6 ZZ, hhll | 6F ZZ rr | 3   | 6   |
| Zero Page, Relative | BBR7 ZZ, hhll | 7F ZZ rr | 3   | 6   |

_Flags Affected_

| N   | V   | T   | B   | D   | I   | Z   | C   |
| --- | --- | --- | --- | --- | --- | --- | --- |
| -   | -   | 0   | -   | -   | -   | -   | -   |

Branch on Carry Clear (BCC)
---------------------------

_Function_ The carry flag in the status register is tested. If it is clear, a branch is taken; if it is set, the instruction immediately following the two-byte BCC instruction is executed. If the branch is taken, a one-byte signed displacement, fetched from the third byte of the instruction, is added to the program counter. Once the branch address has been calculated, the result is loaded into the program counter, transferring control to that location. The allowable range of the displacement is -128 to +127 _from the instruction immediately following the branch_ . Note that BCC determines if the result of a comparison is less than; therefore, BCC is sometimes written as BLT (Branch if Less Than). This opcode takes one extra cycle if the branch is taken, and another extra cycle if a page boundary is crossed in taking the branch.

_Adressing Modes & Opcodes_

| Addressing Mode | Syntax | Opcode | \# of bytes | \# of cycles |
| --- | --- | --- | --- | --- |
| Relative | BCC hhll | 90 rr | 2   | 2   |

_Flags Affected_

| N   | V   | T   | B   | D   | I   | Z   | C   |
| --- | --- | --- | --- | --- | --- | --- | --- |
| -   | -   | 0   | -   | -   | -   | -   | -   |

Branch on Bit Set (BBSi)
------------------------

_Function_ The _i_ th bit value in zero page memory location ZZ is tested. If it is set, a branch is taken; if it is clear, the instruction immediately following the three-byte BBSi instruction is executed. If the branch is taken, a one-byte signed displacement, fetched from the third byte of the instruction, is added to the program counter. Once the branch address has been calculated, the result is loaded into the program counter, transferring control to that location. The allowable range of the displacement is -128 to +127 _from the instruction immediately following the branch_ .

_Adressing Modes & Opcodes_

| Addressing Mode | Syntax | Opcode | \# of bytes | \# of cycles |
| --- | --- | --- | --- | --- |
| Zero Page, Relative | BBS0 ZZ, hhll | 8F ZZ rr | 3   | 6   |
| Zero Page, Relative | BBS1 ZZ, hhll | 9F ZZ rr | 3   | 6   |
| Zero Page, Relative | BBS2 ZZ, hhll | AF ZZ rr | 3   | 6   |
| Zero Page, Relative | BBS3 ZZ, hhll | BF ZZ rr | 3   | 6   |
| Zero Page, Relative | BBS4 ZZ, hhll | CF ZZ rr | 3   | 6   |
| Zero Page, Relative | BBS5 ZZ, hhll | DF ZZ rr | 3   | 6   |
| Zero Page, Relative | BBS6 ZZ, hhll | EF ZZ rr | 3   | 6   |
| Zero Page, Relative | BBS7 ZZ, hhll | FF ZZ rr | 3   | 6   |

_Flags Affected_

| N   | V   | T   | B   | D   | I   | Z   | C   |
| --- | --- | --- | --- | --- | --- | --- | --- |
| -   | -   | 0   | -   | -   | -   | -   | -   |

Branch on Carry Set (BCS)
-------------------------

_Function_ The carry flag in the status register is tested. If it is set, a branch is taken; if it is clear, the instruction immediately following the two-byte BCS instruction is executed. If the branch is taken, a one-byte signed displacement, fetched from the third byte of the instruction, is added to the program counter. Once the branch address has been calculated, the result is loaded into the program counter, transferring control to that location. The allowable range of the displacement is -128 to +127 _from the instruction immediately following the branch_ . Note that BCC determines if the result of a comparison is greater than or equal to; therefore, BCC is sometimes written as BGE (Branch if Greater than or Equal). This opcode takes one extra cycle if the branch is taken, and another extra cycle if a page boundary is crossed in taking the branch.

_Adressing Modes & Opcodes_

| Addressing Mode | Syntax | Opcode | \# of bytes | \# of cycles |
| --- | --- | --- | --- | --- |
| Relative | BCS hhll | B0 rr | 2   | 2   |

_Flags Affected_

| N   | V   | T   | B   | D   | I   | Z   | C   |
| --- | --- | --- | --- | --- | --- | --- | --- |
| -   | -   | 0   | -   | -   | -   | -   | -   |

Branch on Equal (BEQ)
---------------------

_Function_ The zero flag in the status register is tested. If it is set, meaning that the last value tested (which affected the zero flag) was zero, a branch is taken; if it is clear, meaning the value tested was non-zero, the instruction immediately following the two-byte BEQ instruction is executed. If the branch is taken, a one-byte signed displacement, fetched from the third byte of the instruction, is added to the program counter. Once the branch address has been calculated, the result is loaded into the program counter, transferring control to that location. The allowable range of the displacement is -128 to +127 _from the instruction immediately following the branch_ . This opcode takes one extra cycle if the branch is taken, and another extra cycle if a page boundary is crossed in taking the branch.

_Adressing Modes & Opcodes_

| Addressing Mode | Syntax | Opcode | \# of bytes | \# of cycles |
| --- | --- | --- | --- | --- |
| Relative | BEQ hhll | F0 rr | 2   | 2   |

_Flags Affected_

| N   | V   | T   | B   | D   | I   | Z   | C   |
| --- | --- | --- | --- | --- | --- | --- | --- |
| -   | -   | 0   | -   | -   | -   | -   | -   |

Test Memory Bits against Accumulator (BIT)
------------------------------------------

_Function_ BIT sets the status register flags based on the result of two different operations. First, it sets or clears the N flag to reflect the value of the high bit (bit 7) of the data located at the effective address specified by the operand, and sets or clears the V flag to reflect the contents of the next-to-highest bit (bit 6) of the data addressed. Second, it logically ANDs the data located at the effective address with the contents of the accumulator; it changes neither value, but sets the Z flag if the result is zero, or clears it if the result is non-zero.

_Adressing Modes & Opcodes_

| Addressing Mode | Syntax | Opcode | \# of bytes | \# of cycles |
| --- | --- | --- | --- | --- |
| Immediate | BIT #nn | 89 nn | 2   | 2   |
| Zero Page | BIT ZZ | 24 ZZ | 2   | 4   |
| Zero Page, X | BIT ZZ, X | 34 ZZ | 2   | 4   |
| Absolute | BIT hhll | 2C ll hh | 3   | 5   |
| Absolute, X | BIT hhll, X | 3C ll hh | 3   | 5   |

_Flags Affected_

| N   | V   | T   | B   | D   | I   | Z   | C   |
| --- | --- | --- | --- | --- | --- | --- | --- |
| M7  | M6  | 0   | -   | -   | -   | Z   | -   |

Branch on Minus (BMI)
---------------------

_Function_ The negative flag in the status register is tested. If it is set, meaning the high bit of the value which most recently affected the N flag was set, a branch is taken. Since numbers are often stored in two's complement, this instruction can be used to detect negative numbers. If it is clear, the instruction immediately following the two-byte BMI instruction is executed. If the branch is taken, a one-byte signed displacement, fetched from the third byte of the instruction, is added to the program counter. Once the branch address has been calculated, the result is loaded into the program counter, transferring control to that location. The allowable range of the displacement is -128 to +127 _from the instruction immediately following the branch_ . This opcode takes one extra cycle if the branch is taken, and another extra cycle if a page boundary is crossed in taking the branch.

_Adressing Modes & Opcodes_

| Addressing Mode | Syntax | Opcode | \# of bytes | \# of cycles |
| --- | --- | --- | --- | --- |
| Relative | BMI hhll | 30 rr | 2   | 2   |

_Flags Affected_

| N   | V   | T   | B   | D   | I   | Z   | C   |
| --- | --- | --- | --- | --- | --- | --- | --- |
| -   | -   | 0   | -   | -   | -   | -   | -   |

Branch on Not Equal (BNE)
-------------------------

_Function_ The zero flag in the status register is tested. If it is clear, meaning that the last value tested (which affected the zero flag) was zero, a branch is taken; if it is set, meaning the value tested was non-zero, the instruction immediately following the two-byte BNE instruction is executed. If the branch is taken, a one-byte signed displacement, fetched from the third byte of the instruction, is added to the program counter. Once the branch address has been calculated, the result is loaded into the program counter, transferring control to that location. The allowable range of the displacement is -128 to +127 _from the instruction immediately following the branch_ . This opcode takes one extra cycle if the branch is taken, and another extra cycle if a page boundary is crossed in taking the branch.

_Adressing Modes & Opcodes_

| Addressing Mode | Syntax | Opcode | \# of bytes | \# of cycles |
| --- | --- | --- | --- | --- |
| Relative | BNE hhll | D0 rr | 2   | 2   |

_Flags Affected_

| N   | V   | T   | B   | D   | I   | Z   | C   |
| --- | --- | --- | --- | --- | --- | --- | --- |
| -   | -   | 0   | -   | -   | -   | -   | -   |

Branch on Plus (BPL)
--------------------

_Function_ The negative flag in the status register is tested. If it is clear, meaning the high bit of the value which most recently affected the N flag was cleared, a branch is taken. Since numbers are often stored in two's complement, this instruction can be used to detect positive numbers. If it is set, the instruction immediately following the two-byte BPL instruction is executed. If the branch is taken, a one-byte signed displacement, fetched from the third byte of the instruction, is added to the program counter. Once the branch address has been calculated, the result is loaded into the program counter, transferring control to that location. The allowable range of the displacement is -128 to +127 _from the instruction immediately following the branch_ . This opcode takes one extra cycle if the branch is taken, and another extra cycle if a page boundary is crossed in taking the branch.

_Adressing Modes & Opcodes_

| Addressing Mode | Syntax | Opcode | \# of bytes | \# of cycles |
| --- | --- | --- | --- | --- |
| Relative | BPL hhll | 10 rr | 2   | 2   |

_Flags Affected_

| N   | V   | T   | B   | D   | I   | Z   | C   |
| --- | --- | --- | --- | --- | --- | --- | --- |
| -   | -   | 0   | -   | -   | -   | -   | -   |

Branch Always (BRA)
-------------------

_Function_ A branch is always taken; no testing is done. A one-byte signed displacement, fetched from the third byte of the instruction, is added to the program counter. Once the branch address has been calculated, the result is loaded into the program counter, transferring control to that location. The allowable range of the displacement is -128 to +127 _from the instruction immediately following the branch_ . This branch requires one extra cycle if a page boundary is crossed in taking the branch.

_Adressing Modes & Opcodes_

| Addressing Mode | Syntax | Opcode | \# of bytes | \# of cycles |
| --- | --- | --- | --- | --- |
| Relative | BRA hhll | 80 rr | 2   | 4   |

_Flags Affected_

| N   | V   | T   | B   | D   | I   | Z   | C   |
| --- | --- | --- | --- | --- | --- | --- | --- |
| -   | -   | 0   | -   | -   | -   | -   | -   |

Break (BRK)
-----------

_Function_ Forces a software interrupt. BRK is unaffected by the I interrupt disable flag. Although BRK is a one-byte instruction, the program counter (which is pushed onto the stack by the instruction) is incremented by two; this lets you follow the break instruction with a one-byte signature byte indicating which break caused the interrupt. _Be sure to pad BRK with a single byte to allow an RTI (return from interrupt) instruction to execute correctly._ Multiple actions are invoked on a BRK. The program counter is incremented by 2. The high and low bytes of the program counter are pushed onto the stack in order, followed by the status register (P). The program counter is then loaded with the break vector stored at absolute address \\$00FFF6-\\$00FFF7. (Remember, the high byte is stored in \\$00FFF7 and the low byte is stored in \\$00FFF6.) The decimal flag D is cleared, and the I flag is set (to disable hardware IRQ interrupts) after a break is executed. Additionally, the break flag B in the status register value pushed onto the stack is set.

_Adressing Modes & Opcodes_

| Addressing Mode | Syntax | Opcode | \# of bytes | \# of cycles |
| --- | --- | --- | --- | --- |
| Implied | BRK | 00  | 1   | 8   |

_Flags Affected_

| N   | V   | T   | B   | D   | I   | Z   | C   |
| --- | --- | --- | --- | --- | --- | --- | --- |
| -   | -   | 0   | 1   | 0   | 1   | -   | -   |

Branch to Subroutine (BSR)
--------------------------

_Function_ Similar to the Jump to Subroutine (JSR) instruction, Branch to Subroutine allows execution of a subroutine. However, the offset is specified in relative mode instead of as an absolute address. This saves a byte, but takes one more clock cycle than JSR, so its use is discouraged. The current program counter is pushed onto the stack. A one-byte signed displacement, fetched from the second byte of the instruction, is added to the program counter. Once the subroutine address has been calculated, the result is loaded into the program counter, transferring control to that location. The allowable range of the displacement is -128 to +127 _from the instruction immediately following the BSR_ . This opcode takes one extra cycle if a page boundary is crossed in calling the subroutine.

_Adressing Modes & Opcodes_

| Addressing Mode | Syntax | Opcode | \# of bytes | \# of cycles |
| --- | --- | --- | --- | --- |
| Relative | BSR hhll | 44 rr | 2   | 8   |

_Flags Affected_

| N   | V   | T   | B   | D   | I   | Z   | C   |
| --- | --- | --- | --- | --- | --- | --- | --- |
| -   | -   | 0   | -   | -   | -   | -   | -   |

Branch if Overflow Set (BVS)
----------------------------

_Function_ The overflow flag V in the status register is tested. If it is set, a branch is taken; if it is clear, the instruction immediately following the two-byte BVS instruction is executed. If the branch is taken, a one-byte signed displacement, fetched from the third byte of the instruction, is added to the program counter. Once the branch address has been calculated, the result is loaded into the program counter, transferring control to that location. The allowable range of the displacement is -128 to +127 _from the instruction immediately following the branch_ . BVS is almost exclusively used to check that a two's complement arithmetic calculation has overflowed. This opcode takes one extra cycle if the branch is taken, and another extra cycle if a page boundary is crossed in taking the branch.

_Adressing Modes & Opcodes_

| Addressing Mode | Syntax | Opcode | \# of bytes | \# of cycles |
| --- | --- | --- | --- | --- |
| Relative | BVS hhll | 70 rr | 2   | 2   |

_Flags Affected_

| N   | V   | T   | B   | D   | I   | Z   | C   |
| --- | --- | --- | --- | --- | --- | --- | --- |
| -   | -   | 0   | -   | -   | -   | -   | -   |

Branch if Overflow Clear (BVC)
------------------------------

_Function_ The overflow flag V in the status register is tested. If it is clear, a branch is taken; if it is set, the instruction immediately following the two-byte BVC instruction is executed. If the branch is taken, a one-byte signed displacement, fetched from the third byte of the instruction, is added to the program counter. Once the branch address has been calculated, the result is loaded into the program counter, transferring control to that location. The allowable range of the displacement is -128 to +127 _from the instruction immediately following the branch_ . BVC is almost exclusively used to check that a two's complement arithmetic calculation has not overflowed. This opcode takes one extra cycle if the branch is taken, and another extra cycle if a page boundary is crossed in taking the branch.

_Adressing Modes & Opcodes_

| Addressing Mode | Syntax | Opcode | \# of bytes | \# of cycles |
| --- | --- | --- | --- | --- |
| Relative | BVC hhll | 50 rr | 2   | 2   |

_Flags Affected_

| N   | V   | T   | B   | D   | I   | Z   | C   |
| --- | --- | --- | --- | --- | --- | --- | --- |
| -   | -   | 0   | -   | -   | -   | -   | -   |

Clear Carry Flag (CLC)
----------------------

_Function_ The carry flag C in the status register is set to 0.

_Adressing Modes & Opcodes_

| Addressing Mode | Syntax | Opcode | \# of bytes | \# of cycles |
| --- | --- | --- | --- | --- |
| Implied | CLC | 18  | 1   | 2   |

_Flags Affected_

| N   | V   | T   | B   | D   | I   | Z   | C   |
| --- | --- | --- | --- | --- | --- | --- | --- |
| -   | -   | 0   | -   | -   | -   | -   | 0   |

Clear Accumulator (CLA)
-----------------------

_Function_ The accumulator is set to \\$#00.

_Adressing Modes & Opcodes_

| Addressing Mode | Syntax | Opcode | \# of bytes | \# of cycles |
| --- | --- | --- | --- | --- |
| Implied | CLA | 62  | 1   | 2   |

_Flags Affected_

| N   | V   | T   | B   | D   | I   | Z   | C   |
| --- | --- | --- | --- | --- | --- | --- | --- |
| -   | -   | 0   | -   | -   | -   | -   | -   |

Clear Decimal Flag (CLD)
------------------------

_Function_ The decimal flag D in the status register is set to 0, returning the processor to binary arithmetic mode.

_Adressing Modes & Opcodes_

| Addressing Mode | Syntax | Opcode | \# of bytes | \# of cycles |
| --- | --- | --- | --- | --- |
| Implied | CLD | D8  | 1   | 2   |

_Flags Affected_

| N   | V   | T   | B   | D   | I   | Z   | C   |
| --- | --- | --- | --- | --- | --- | --- | --- |
| -   | -   | 0   | -   | 0   | -   | -   | -   |

Clear Interrupt Disable Flag (CLI)
----------------------------------

_Function_ The interrupt disable flag I in the status register is set to 0. This re-enables hardware interrupt (IRQ) processing.

_Adressing Modes & Opcodes_

| Addressing Mode | Syntax | Opcode | \# of bytes | \# of cycles |
| --- | --- | --- | --- | --- |
| Implied | CLI | 58  | 1   | 2   |

_Flags Affected_

| N   | V   | T   | B   | D   | I   | Z   | C   |
| --- | --- | --- | --- | --- | --- | --- | --- |
| -   | -   | 0   | -   | -   | 0   | -   | -   |

Clear Overflow Flag (CLV)
-------------------------

_Function_ The overflow flag V in the status register is set to 0.

_Adressing Modes & Opcodes_

| Addressing Mode | Syntax | Opcode | \# of bytes | \# of cycles |
| --- | --- | --- | --- | --- |
| Implied | CLV | B8  | 1   | 2   |

_Flags Affected_

| N   | V   | T   | B   | D   | I   | Z   | C   |
| --- | --- | --- | --- | --- | --- | --- | --- |
| -   | 0   | 0   | -   | -   | -   | -   | -   |

Clear Y Register (CLY)
----------------------

_Function_ The Y register is set to #\\$00.

_Adressing Modes & Opcodes_

| Addressing Mode | Syntax | Opcode | \# of bytes | \# of cycles |
| --- | --- | --- | --- | --- |
| Implied | CLY | C2  | 1   | 2   |

_Flags Affected_

| N   | V   | T   | B   | D   | I   | Z   | C   |
| --- | --- | --- | --- | --- | --- | --- | --- |
| -   | -   | 0   | -   | -   | -   | -   | -   |

Clear X Register (CLX)
----------------------

_Function_ The X register is set to #\\$00.

_Adressing Modes & Opcodes_

| Addressing Mode | Syntax | Opcode | \# of bytes | \# of cycles |
| --- | --- | --- | --- | --- |
| Implied | CLX | 82  | 1   | 2   |

_Flags Affected_

| N   | V   | T   | B   | D   | I   | Z   | C   |
| --- | --- | --- | --- | --- | --- | --- | --- |
| -   | -   | 0   | -   | -   | -   | -   | -   |

Compare X Register with Memory (CPX)
------------------------------------

_Function_ Subtract the data located at the effective address specified by the operand from the contents of the X register, setting the carry, zero, and negative flags based on the result, but without altering the contents of either the memory location or the accumulator. The comparison is of unsigned binary values only (decimal mode is ignored), and the result is not saved.

_Adressing Modes & Opcodes_

| Addressing Mode | Syntax | Opcode | \# of bytes | \# of cycles |
| --- | --- | --- | --- | --- |
| Immediate | CPX #nn | E0 nn | 2   | 2   |
| Zero Page | CPX ZZ | E4 ZZ | 2   | 4   |
| Absolute | CPX hhll | EC ll hh | 3   | 5   |

_Flags Affected_

| N   | V   | T   | B   | D   | I   | Z   | C   |
| --- | --- | --- | --- | --- | --- | --- | --- |
| N   | -   | 0   | -   | -   | -   | Z   | C   |

Change Speed High (CSH)
-----------------------

_Function_ Sets the HuC6280 to "high speed," or normal speed mode. The only use for this instruction is after a system reset, to ensure that the processor is in its high speed mode.

_Adressing Modes & Opcodes_

| Addressing Mode | Syntax | Opcode | \# of bytes | \# of cycles |
| --- | --- | --- | --- | --- |
| Implied | CSH | D4  | 1   | ??  |

_Flags Affected_

| N   | V   | T   | B   | D   | I   | Z   | C   |
| --- | --- | --- | --- | --- | --- | --- | --- |
| -   | -   | 0   | -   | -   | -   | -   | -   |

Change Speed Low (CSL)
----------------------

_Function_ Sets the HuC6280 to low speed. The only use for this instruction appears to be for the US "country check" code; it does not appear anywhere else in HuC6280 code. Its use is discouraged.

_Adressing Modes & Opcodes_

| Addressing Mode | Syntax | Opcode | \# of bytes | \# of cycles |
| --- | --- | --- | --- | --- |
| Implied | CSL | 54  | 1   | ??  |

_Flags Affected_

| N   | V   | T   | B   | D   | I   | Z   | C   |
| --- | --- | --- | --- | --- | --- | --- | --- |
| -   | -   | 0   | -   | -   | -   | -   | -   |

Compare Accumulator with Memory (CMP)
-------------------------------------

_Function_ Subtract the data located at the effective address specified by the operand from the contents of the accumulator, setting the carry, zero, and negative flags based on the result, but without altering the contents of either the memory location or the accumulator. The comparison is of unsigned binary values only (decimal mode is ignored), and the result is not saved.

_Adressing Modes & Opcodes_

| Addressing Mode | Syntax | Opcode | \# of bytes | \# of cycles |
| --- | --- | --- | --- | --- |
| Immediate | CMP #nn | C9 nn | 2   | 2   |
| Zero Page | CMP ZZ | C5 ZZ | 2   | 4   |
| Zero Page, X | CMP ZZ, X | D5 ZZ | 2   | 4   |
| Indirect | CMP (ZZ) | D2 ZZ | 2   | 7   |
| Indexed Indirect, X | CMP (ZZ, X) | C1 ZZ | 2   | 7   |
| Indirect Indexed, Y | CMP (ZZ), Y | D1 ZZ | 2   | 7   |
| Absolute | CMP hhll | CD ll hh | 3   | 5   |
| Absolute, X | CMP hhll, X | DD ll hh | 3   | 5   |
| Absolute, Y | CMP hhll, Y | D9 ll hh | 3   | 5   |

_Flags Affected_

| N   | V   | T   | B   | D   | I   | Z   | C   |
| --- | --- | --- | --- | --- | --- | --- | --- |
| N   | -   | 0   | -   | -   | -   | Z   | C   |

Decrement X (DEX)
-----------------

_Function_ Decrement by one the contents of the X register (subtract one from the value). DEX neither affects nor is affected by the carry flag.

_Adressing Modes & Opcodes_

| Addressing Mode | Syntax | Opcode | \# of bytes | \# of cycles |
| --- | --- | --- | --- | --- |
| Implied | DEX | CA  | 1   | 2   |

_Flags Affected_

| N   | V   | T   | B   | D   | I   | Z   | C   |
| --- | --- | --- | --- | --- | --- | --- | --- |
| N   | -   | 0   | -   | -   | -   | Z   | -   |

Decrement (DEC)
---------------

_Function_ Decrement by one the contents of the location specified by the operand (subtract one from the value). DEC neither affects nor is affected by the carry flag.

_Adressing Modes & Opcodes_

| Addressing Mode | Syntax | Opcode | \# of bytes | \# of cycles |
| --- | --- | --- | --- | --- |
| Zero Page | DEC ZZ | C6 ZZ | 2   | 6   |
| Zero Page, X | DEC ZZ, X | D6 ZZ | 2   | 6   |
| Absolute | DEC hhll | CE ll hh | 3   | 7   |
| Absolute, X | DEC hhll, X | DE ll hh | 3   | 7   |
| Accumulator | DEC A | 3A  | 1   | 2   |

_Flags Affected_

| N   | V   | T   | B   | D   | I   | Z   | C   |
| --- | --- | --- | --- | --- | --- | --- | --- |
| N   | -   | 0   | -   | -   | -   | Z   | -   |

Compare Y Register with Memory (CPY)
------------------------------------

_Function_ Subtract the data located at the effective address specified by the operand from the contents of the Y register, setting the carry, zero, and negative flags based on the result, but without altering the contents of either the memory location or the accumulator. The comparison is of unsigned binary values only (decimal mode is ignored), and the result is not saved.

_Adressing Modes & Opcodes_

| Addressing Mode | Syntax | Opcode | \# of bytes | \# of cycles |
| --- | --- | --- | --- | --- |
| Immediate | CPY #nn | C0 nn | 2   | 2   |
| Zero Page | CPY ZZ | C4 ZZ | 2   | 4   |
| Absolute | CPY hhll | CC ll hh | 3   | 5   |

_Flags Affected_

| N   | V   | T   | B   | D   | I   | Z   | C   |
| --- | --- | --- | --- | --- | --- | --- | --- |
| N   | -   | 0   | -   | -   | -   | Z   | C   |

Exclusive OR Accumulator with Memory (EOR)
------------------------------------------

_Function_ Bitwise logical Exclusive OR (XOR) the data located at the effective address specified by the operand with the contents of the accumulator. Each bit in the accumulator is XORed with the corresponding bit in memory, with the result being stored in the respective accumulator bit.

_Adressing Modes & Opcodes_

| Addressing Mode | Syntax | Opcode | \# of bytes | \# of cycles |
| --- | --- | --- | --- | --- |
| Immediate | EOR #nn | 49 nn | 2   | 2   |
| Zero Page | EOR ZZ | 45 ZZ | 2   | 4   |
| Zero Page, X | EOR ZZ, X | 55 ZZ | 2   | 4   |
| Indirect | EOR (ZZ) | 52 ZZ | 2   | 7   |
| Indexed Indirect, X | EOR (ZZ, X) | 41 ZZ | 2   | 7   |
| Indirect Indexed, Y | EOR (ZZ), Y | 51 ZZ | 2   | 7   |
| Absolute | EOR hhll | 4D ll hh | 3   | 5   |
| Absolute, X | EOR hhll, X | 5D ll hh | 3   | 5   |
| Absolute, Y | EOR hhll, Y | 59 ll hh | 3   | 5   |

_Flags Affected_

| N   | V   | T   | B   | D   | I   | Z   | C   |
| --- | --- | --- | --- | --- | --- | --- | --- |
| N   | -   | 0   | -   | -   | -   | Z   | -   |

Increment (INC)
---------------

_Function_ Increments contents of the location specified by the operand (add one to the value). INC neither affects nor is affected by the carry flag.

_Adressing Modes & Opcodes_

| Addressing Mode | Syntax | Opcode | \# of bytes | \# of cycles |
| --- | --- | --- | --- | --- |
| Zero Page | INC ZZ | E6 ZZ | 2   | 6   |
| Zero Page, X | INC ZZ, X | F6 ZZ | 2   | 6   |
| Absolute | INC hhll | EE ll hh | 3   | 7   |
| Absolute, X | INC hhll, X | FE ll hh | 3   | 7   |
| Accumulator | INC A | 1A  | 1   | 2   |

_Flags Affected_

| N   | V   | T   | B   | D   | I   | Z   | C   |
| --- | --- | --- | --- | --- | --- | --- | --- |
| N   | -   | 0   | -   | -   | -   | Z   | -   |

Increment X (INX)
-----------------

_Function_ Increment by one contents of the X register (add one to the value). INX neither affects nor is affected by the carry flag.

_Adressing Modes & Opcodes_

| Addressing Mode | Syntax | Opcode | \# of bytes | \# of cycles |
| --- | --- | --- | --- | --- |
| Implied | INX | E8  | 1   | 2   |

_Flags Affected_

| N   | V   | T   | B   | D   | I   | Z   | C   |
| --- | --- | --- | --- | --- | --- | --- | --- |
| N   | -   | 0   | -   | -   | -   | Z   | -   |

Decrement Y (DEY)
-----------------

_Function_ Decrement by one the contents of the Y register (subtract one from the value). DEY neither affects nor is affected by the carry flag.

_Adressing Modes & Opcodes_

| Addressing Mode | Syntax | Opcode | \# of bytes | \# of cycles |
| --- | --- | --- | --- | --- |
| Implied | DEY | 88  | 1   | 2   |

_Flags Affected_

| N   | V   | T   | B   | D   | I   | Z   | C   |
| --- | --- | --- | --- | --- | --- | --- | --- |
| N   | -   | 0   | -   | -   | -   | Z   | -   |

Increment Y (INY)
-----------------

_Function_ Increment by one contents of the Y register (add one to the value). INY neither affects nor is affected by the carry flag.

_Adressing Modes & Opcodes_

| Addressing Mode | Syntax | Opcode | \# of bytes | \# of cycles |
| --- | --- | --- | --- | --- |
| Implied | INY | C8  | 1   | 2   |

_Flags Affected_

| N   | V   | T   | B   | D   | I   | Z   | C   |
| --- | --- | --- | --- | --- | --- | --- | --- |
| N   | -   | 0   | -   | -   | -   | Z   | -   |

Jump (JMP)
----------

_Function_ Transfer control to the address specified by the operand field. The program counter is loaded with the target address.

_Adressing Modes & Opcodes_

| Addressing Mode | Syntax | Opcode | \# of bytes | \# of cycles |
| --- | --- | --- | --- | --- |
| Absolute | JMP hhll | 4C ll hh | 3   | 4   |
| Absolute Indirect | JMP (hhll) | 6C ll hh | 3   | 7   |
| Absolute Indirect X | JMP hhll, X | 7C ll hh | 3   | 7   |

_Flags Affected_

| N   | V   | T   | B   | D   | I   | Z   | C   |
| --- | --- | --- | --- | --- | --- | --- | --- |
| -   | -   | 0   | -   | -   | -   | -   | -   |

Jump to Subroutine (JSR)
------------------------

_Function_ Transfer control to the subroutine at the location specified by the operand, after first pushing the current program counter value onto the stack as a return address. The value of the PC which is pushed onto the stack is the location of the last (third) byte of the JSR instruction, _not_ the address of the next opcode.

_Adressing Modes & Opcodes_

| Addressing Mode | Syntax | Opcode | \# of bytes | \# of cycles |
| --- | --- | --- | --- | --- |
| Absolute | JSR hhll | 20 ll hh | 3   | 7   |

_Flags Affected_

| N   | V   | T   | B   | D   | I   | Z   | C   |
| --- | --- | --- | --- | --- | --- | --- | --- |
| -   | -   | 0   | -   | -   | -   | -   | -   |

Load Accumulator from Memory (LDA)
----------------------------------

_Function_ Load the accumulator with the data located at the effective address specified by the operand.

_Adressing Modes & Opcodes_

| Addressing Mode | Syntax | Opcode | \# of bytes | \# of cycles |
| --- | --- | --- | --- | --- |
| Immediate | LDA #nn | A9 nn | 2   | 2   |
| Zero Page | LDA ZZ | A5 ZZ | 2   | 4   |
| Zero Page, X | LDA ZZ, X | B5 ZZ | 2   | 4   |
| Indirect | LDA (ZZ) | B2 ZZ | 2   | 7   |
| Indexed Indirect, X | LDA (ZZ, X) | A1 ZZ | 2   | 7   |
| Indirect Indexed, Y | LDA (ZZ), Y | B1 ZZ | 2   | 7   |
| Absolute | LDA hhll | AD ll hh | 3   | 5   |
| Absolute, X | LDA hhll, X | BD ll hh | 3   | 5   |
| Absolute, Y | LDA hhll, Y | B9 ll hh | 3   | 5   |

_Flags Affected_

| N   | V   | T   | B   | D   | I   | Z   | C   |
| --- | --- | --- | --- | --- | --- | --- | --- |
| N   | -   | 0   | -   | -   | -   | Z   | -   |

Load X Register from Memory (LDX)
---------------------------------

_Function_ Load the X register with the data located at the effective address specified by the operand.

_Adressing Modes & Opcodes_

| Addressing Mode | Syntax | Opcode | \# of bytes | \# of cycles |
| --- | --- | --- | --- | --- |
| Immediate | LDX #nn | A2 nn | 2   | 2   |
| Zero Page | LDX ZZ | A6 ZZ | 2   | 4   |
| Zero Page, Y | LDX ZZ, Y | B6 ZZ | 2   | 4   |
| Absolute | LDX hhll | AE ll hh | 3   | 5   |
| Absolute, Y | LDX hhll, Y | BE ll hh | 3   | 5   |

_Flags Affected_

| N   | V   | T   | B   | D   | I   | Z   | C   |
| --- | --- | --- | --- | --- | --- | --- | --- |
| N   | -   | 0   | -   | -   | -   | Z   | -   |

Load Y Register from Memory (LDY)
---------------------------------

_Function_ Load the Y register with the data located at the effective address specified by the operand.

_Adressing Modes & Opcodes_

| Addressing Mode | Syntax | Opcode | \# of bytes | \# of cycles |
| --- | --- | --- | --- | --- |
| Immediate | LDY #nn | A0 nn | 2   | 2   |
| Zero Page | LDY ZZ | A4 ZZ | 2   | 4   |
| Zero Page, X | LDY ZZ, Y | B4 ZZ | 2   | 4   |
| Absolute | LDY hhll | AC ll hh | 3   | 5   |
| Absolute, X | LDY hhll, Y | BC ll hh | 3   | 5   |

_Flags Affected_

| N   | V   | T   | B   | D   | I   | Z   | C   |
| --- | --- | --- | --- | --- | --- | --- | --- |
| N   | -   | 0   | -   | -   | -   | Z   | -   |

Logical Shift Memory or Accumulator Right (LSR)
-----------------------------------------------

_Function_ Logical shift the contents of the location specified by the operand right one bit. That is, bit zero takes on the value originally found in bit one, bit one takes the value originally in bit two, and so on; bit 7 is cleared; bit 0 is transferred into the carry flag. The arithmetic result of the operation is an unsigned division by two.

_Adressing Modes & Opcodes_

| Addressing Mode | Syntax | Opcode | \# of bytes | \# of cycles |
| --- | --- | --- | --- | --- |
| Zero Page | LSR ZZ | 46 ZZ | 2   | 6   |
| Zero Page, X | LSR ZZ, X | 56 ZZ | 2   | 6   |
| Absolute | LSR hhll | 4E ll hh | 3   | 7   |
| Absolute, X | LSR hhll, X | 5E ll hh | 3   | 7   |
| Accumulator | LSR A | 4A ll hh | 1   | 2   |

_Flags Affected_

| N   | V   | T   | B   | D   | I   | Z   | C   |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 0   | -   | 0   | -   | -   | -   | Z   | C   |

Or Accumulator with Memory (ORA)
--------------------------------

_Function_ Bitwise logical OR the data located at the effective address specified by the operand with the contents of the accumulator. Each bit in the accumulator is ORed with the corresponding bit in memory, with the result being stored in the respective accumulator bit.

_Adressing Modes & Opcodes_

| Addressing Mode | Syntax | Opcode | \# of bytes | \# of cycles |
| --- | --- | --- | --- | --- |
| Immediate | ORA #nn | 09 nn | 2   | 2   |
| Zero Page | ORA ZZ | 05 ZZ | 2   | 4   |
| Zero Page, X | ORA ZZ, X | 15 ZZ | 2   | 4   |
| Indirect | ORA (ZZ) | 12 ZZ | 2   | 7   |
| Indexed Indirect, X | ORA (ZZ, X) | 01 ZZ | 2   | 7   |
| Indirect Indexed, Y | ORA (ZZ), Y | 11 ZZ | 2   | 7   |
| Absolute | ORA hhll | 0D ll hh | 3   | 5   |
| Absolute, X | ORA hhll, X | 1D ll hh | 3   | 5   |
| Absolute, Y | ORA hhll, Y | 19 ll hh | 3   | 5   |

_Flags Affected_

| N   | V   | T   | B   | D   | I   | Z   | C   |
| --- | --- | --- | --- | --- | --- | --- | --- |
| N   | -   | 0   | -   | -   | -   | Z   | -   |

No Operation (NOP)
------------------

_Function_ NOP performs no action, and is often used for timing loops or temporarily removing certain instructions.

_Adressing Modes & Opcodes_

| Addressing Mode | Syntax | Opcode | \# of bytes | \# of cycles |
| --- | --- | --- | --- | --- |
| Implied | NOP | EA  | 1   | 2   |

_Flags Affected_

| N   | V   | T   | B   | D   | I   | Z   | C   |
| --- | --- | --- | --- | --- | --- | --- | --- |
| -   | -   | 0   | -   | -   | -   | -   | -   |

Push Accumulator (PHA)
----------------------

_Function_ Push the accumulator onto the stack.

_Adressing Modes & Opcodes_

| Addressing Mode | Syntax | Opcode | \# of bytes | \# of cycles |
| --- | --- | --- | --- | --- |
| Stack Push | PHA | 48  | 1   | 3   |

_Flags Affected_

| N   | V   | T   | B   | D   | I   | Z   | C   |
| --- | --- | --- | --- | --- | --- | --- | --- |
| -   | -   | 0   | -   | -   | -   | -   | -   |

Push Processor Status Register (PHP)
------------------------------------

_Function_ Push the process status register P onto the stack.

_Adressing Modes & Opcodes_

| Addressing Mode | Syntax | Opcode | \# of bytes | \# of cycles |
| --- | --- | --- | --- | --- |
| Stack Push | PHP | 08  | 1   | 3   |

_Flags Affected_

| N   | V   | T   | B   | D   | I   | Z   | C   |
| --- | --- | --- | --- | --- | --- | --- | --- |
| -   | -   | 0   | -   | -   | -   | -   | -   |

Push X Register (PHX)
---------------------

_Function_ Push the X register onto the stack.

_Adressing Modes & Opcodes_

| Addressing Mode | Syntax | Opcode | \# of bytes | \# of cycles |
| --- | --- | --- | --- | --- |
| Stack Push | PHX | DA  | 1   | 3   |

_Flags Affected_

| N   | V   | T   | B   | D   | I   | Z   | C   |
| --- | --- | --- | --- | --- | --- | --- | --- |
| -   | -   | 0   | -   | -   | -   | -   | -   |

Push Y Register (PHY)
---------------------

_Function_ Push the Y register onto the stack.

_Adressing Modes & Opcodes_

| Addressing Mode | Syntax | Opcode | \# of bytes | \# of cycles |
| --- | --- | --- | --- | --- |
| Stack Push | PHY | 5A  | 1   | 3   |

_Flags Affected_

| N   | V   | T   | B   | D   | I   | Z   | C   |
| --- | --- | --- | --- | --- | --- | --- | --- |
| -   | -   | 0   | -   | -   | -   | -   | -   |

Pull Accumulator (PLA)
----------------------

_Function_ Pull the value on the top of the stack into the accumulator. The previous contents of the accumulator are destroyed.

_Adressing Modes & Opcodes_

| Addressing Mode | Syntax | Opcode | \# of bytes | \# of cycles |
| --- | --- | --- | --- | --- |
| Stack Pull | PLA | 68  | 1   | 4   |

_Flags Affected_

| N   | V   | T   | B   | D   | I   | Z   | C   |
| --- | --- | --- | --- | --- | --- | --- | --- |
| N   | -   | 0   | -   | -   | -   | Z   | -   |

Pull Processor Status Register (PLP)
------------------------------------

_Function_ Pull the value on the top of the stack into the processor status register P. The previous contents of the status register are destroyed.

_Adressing Modes & Opcodes_

| Addressing Mode | Syntax | Opcode | \# of bytes | \# of cycles |
| --- | --- | --- | --- | --- |
| Stack Pull | PLP | 28  | 1   | 4   |

_Flags Affected_

| N   | V   | T   | B   | D   | I   | Z   | C   |
| --- | --- | --- | --- | --- | --- | --- | --- |
|     | Restored |     |     |     |     |     |     |     |

Pull X Register (PLX)
---------------------

_Function_ Pull the value on the top of the stack into the X register. The previous contents of the X register are destroyed.

_Adressing Modes & Opcodes_

| Addressing Mode | Syntax | Opcode | \# of bytes | \# of cycles |
| --- | --- | --- | --- | --- |
| Stack Pull | PLX | FA  | 1   | 4   |

_Flags Affected_

| N   | V   | T   | B   | D   | I   | Z   | C   |
| --- | --- | --- | --- | --- | --- | --- | --- |
| N   | -   | 0   | -   | -   | -   | Z   | -   |

Pull Y Register (PLY)
---------------------

_Function_ Pull the value on the top of the stack into the Y register. The previous contents of the Y register are destroyed.

_Adressing Modes & Opcodes_

| Addressing Mode | Syntax | Opcode | \# of bytes | \# of cycles |
| --- | --- | --- | --- | --- |
| Stack Pull | PLY | 7A  | 1   | 4   |

_Flags Affected_

| N   | V   | T   | B   | D   | I   | Z   | C   |
| --- | --- | --- | --- | --- | --- | --- | --- |
| N   | -   | 0   | -   | -   | -   | Z   | -   |

Rotate Memory or Accumulator Left (ROL)
---------------------------------------

_Function_ Rotate the contents of the location specified by the operand left one bit. That is, bit one takes on the value originally found in bit zero, bit two takes the value originally in bit one, and so on; bit 0 takes on the value in the carry flag; bit 7 is transferred into the carry.

_Adressing Modes & Opcodes_

| Addressing Mode | Syntax | Opcode | \# of bytes | \# of cycles |
| --- | --- | --- | --- | --- |
| Zero Page | ROL ZZ | 26 ZZ | 2   | 6   |
| Zero Page, X | ROL ZZ, X | 36 ZZ | 2   | 6   |
| Absolute | ROL hhll | 2E ll hh | 3   | 7   |
| Absolute, X | ROL hhll, X | 3E ll hh | 3   | 7   |
| Accumulator | ROL A | 2A ll hh | 1   | 2   |

_Flags Affected_

| N   | V   | T   | B   | D   | I   | Z   | C   |
| --- | --- | --- | --- | --- | --- | --- | --- |
| N   | -   | 0   | -   | -   | -   | Z   | C   |

Reset Memory Bit i (RMBi)
-------------------------

_Function_ Clear the specified bit in the zero page memory location specified in the operand. The bit to clear is specified by a number concatenated to the end of the mnemonic, resulting in 8 distinct Opcodes.

_Adressing Modes & Opcodes_

| Addressing Mode | Syntax | Opcode | \# of bytes | \# of cycles |
| --- | --- | --- | --- | --- |
| Zero page | RMB0 ZZ | 07 ZZ | 2   | 7   |
| Zero page | RMB1 ZZ | 17 ZZ | 2   | 7   |
| Zero page | RMB2 ZZ | 27 ZZ | 2   | 7   |
| Zero page | RMB3 ZZ | 37 ZZ | 2   | 7   |
| Zero page | RMB4 ZZ | 47 ZZ | 2   | 7   |
| Zero page | RMB5 ZZ | 57 ZZ | 2   | 7   |
| Zero page | RMB6 ZZ | 67 ZZ | 2   | 7   |
| Zero page | RMB7 ZZ | 77 ZZ | 2   | 7   |

_Flags Affected_

| N   | V   | T   | B   | D   | I   | Z   | C   |
| --- | --- | --- | --- | --- | --- | --- | --- |
| -   | -   | 0   | -   | -   | -   | -   | -   |

Rotate Memory or Accumulator Right (ROR)
----------------------------------------

_Function_ Rotate the contents of the location specified by the operand right one bit. That is, bit zero takes on the value originally found in bit one, bit one takes the value originally in bit two, and so on; bit 7 takes on the value in the carry flag; bit 0 is transferred into the carry.

_Adressing Modes & Opcodes_

| Addressing Mode | Syntax | Opcode | \# of bytes | \# of cycles |
| --- | --- | --- | --- | --- |
| Zero Page | ROR ZZ | 66 ZZ | 2   | 6   |
| Zero Page, X | ROR ZZ, X | 76 ZZ | 2   | 6   |
| Absolute | ROR hhll | 6E ll hh | 3   | 7   |
| Absolute, X | ROR hhll, X | 7E ll hh | 3   | 7   |
| Accumulator | ROR A | 6A ll hh | 1   | 2   |

_Flags Affected_

| N   | V   | T   | B   | D   | I   | Z   | C   |
| --- | --- | --- | --- | --- | --- | --- | --- |
| N   | -   | 0   | -   | -   | -   | Z   | C   |

Return from Interrupt (RTI)
---------------------------

_Function_ Pull the status register and the program counter from the stack in order. Normally used to return from an interrupt call (such as BRK), this instruction can also be used to pull the status register P, and the program counter low and high bytes from the stack into the P and program counter registers.

_Adressing Modes & Opcodes_

| Addressing Mode | Syntax | Opcode | \# of bytes | \# of cycles |
| --- | --- | --- | --- | --- |
| Stack (RTI) | RTI | 40  | 1   | 7   |

_Flags Affected_

| N   | V   | T   | B   | D   | I   | Z   | C   |
| --- | --- | --- | --- | --- | --- | --- | --- |
|     | Restored |     |     |     |     |     |     |     |

Return from Subroutine (RTS)
----------------------------

_Function_ Pull the program counter from the stack, incrementing the 16-bit value by one before loading the program counter with it. The low byte of the program counter is pulled from the stack first, followed by the high byte.

_Adressing Modes & Opcodes_

| Addressing Mode | Syntax | Opcode | \# of bytes | \# of cycles |
| --- | --- | --- | --- | --- |
| Stack (RTS) | RTS | 60  | 1   | 7   |

_Flags Affected_

| N   | V   | T   | B   | D   | I   | Z   | C   |
| --- | --- | --- | --- | --- | --- | --- | --- |
| -   | -   | 0   | -   | -   | -   | -   | -   |

Swap Accumulator and X Register (SAX)
-------------------------------------

_Function_ The values of the accumulator and the X Register are swapped.

_Adressing Modes & Opcodes_

| Addressing Mode | Syntax | Opcode | \# of bytes | \# of cycles |
| --- | --- | --- | --- | --- |
| Implied | SAX | 22  | 1   | 3   |

_Flags Affected_

| N   | V   | T   | B   | D   | I   | Z   | C   |
| --- | --- | --- | --- | --- | --- | --- | --- |
| -   | -   | 0   | -   | -   | -   | -   | -   |

Swap Accumulator and Y Register (SAY)
-------------------------------------

_Function_ The values of the accumulator and the Y Register are swapped.

_Adressing Modes & Opcodes_

| Addressing Mode | Syntax | Opcode | \# of bytes | \# of cycles |
| --- | --- | --- | --- | --- |
| Implied | SAY | 42  | 1   | 3   |

_Flags Affected_

| N   | V   | T   | B   | D   | I   | Z   | C   |
| --- | --- | --- | --- | --- | --- | --- | --- |
| -   | -   | 0   | -   | -   | -   | -   | -   |

Subtract with Borrow from Accumulator (SBC)
-------------------------------------------

_Function_ Subtract the data located at the effective address specified by the operand to the contents of the accumulator. Subtract one more from the result if the carry flag is set, and store the final result in the accumulator. This opcode takes one extra cycle if the decimal mode flag D is set.

_Adressing Modes & Opcodes_

| Addressing Mode | Syntax | Opcode | \# of bytes | \# of cycles |
| --- | --- | --- | --- | --- |
| Immediate | SBC #nn | E9 nn | 2   | 2   |
| Zero Page | SBC ZZ | E5 ZZ | 2   | 4   |
| Zero Page, X | SBC ZZ, X | F5 ZZ | 2   | 4   |
| Indirect | SBC (ZZ) | F2 ZZ | 2   | 7   |
| Indexed Indirect, X | SBC (ZZ, X) | E1 ZZ | 2   | 7   |
| Indirect Indexed, Y | SBC (ZZ), Y | F1 ZZ | 2   | 7   |
| Absolute | SBC hhll | ED ll hh | 3   | 5   |
| Absolute, X | SBC hhll, X | FD ll hh | 3   | 5   |
| Absolute, Y | SBC hhll, Y | F9 ll hh | 3   | 5   |

_Flags Affected_

| N   | V   | T   | B   | D   | I   | Z   | C   |
| --- | --- | --- | --- | --- | --- | --- | --- |
| N   | V   | 0   | -   | -   | -   | Z   | C   |

Set Decimal Mode Flag (SED)
---------------------------

_Function_ The decimal mode flag D in the status register is set to 1. This enables BCD arithmetic.

_Adressing Modes & Opcodes_

| Addressing Mode | Syntax | Opcode | \# of bytes | \# of cycles |
| --- | --- | --- | --- | --- |
| Implied | SED | F8  | 1   | 2   |

_Flags Affected_

| N   | V   | T   | B   | D   | I   | Z   | C   |
| --- | --- | --- | --- | --- | --- | --- | --- |
| -   | -   | 0   | -   | 1   | -   | -   | -   |

Set Carry Flag (SEC)
--------------------

_Function_ The carry flag C in the status register is set to 1.

_Adressing Modes & Opcodes_

| Addressing Mode | Syntax | Opcode | \# of bytes | \# of cycles |
| --- | --- | --- | --- | --- |
| Implied | SEC | 38  | 1   | 2   |

_Flags Affected_

| N   | V   | T   | B   | D   | I   | Z   | C   |
| --- | --- | --- | --- | --- | --- | --- | --- |
| -   | -   | 0   | -   | -   | -   | -   | 1   |

Set Interrupt Disable Flag (SEI)
--------------------------------

_Function_ The interrupt disable flag I in the status register is set to 1. This disables hardware interrupt processing.

_Adressing Modes & Opcodes_

| Addressing Mode | Syntax | Opcode | \# of bytes | \# of cycles |
| --- | --- | --- | --- | --- |
| Implied | SEI | 78  | 1   | 2   |

_Flags Affected_

| N   | V   | T   | B   | D   | I   | Z   | C   |
| --- | --- | --- | --- | --- | --- | --- | --- |
| -   | -   | 0   | -   | -   | 1   | -   | -   |

Set T Flag (SET)
----------------

_Function_ The T flag in the status register is set to 1. The T flag is called the "Memory Operation Flag;", when this flag is set all the instructions that normally use the A register act differently, I don't know exactly if all the instructions are affected but I'm sure for AND, EOR, OR & ADC. In place of using the A register the instruction use the memory location in ZP pointed by the X register, so for example if you use SET followed by ADC #10, the CPU will do ZP\[X\] = ZP\[X\] + 10.

_Adressing Modes & Opcodes_

| Addressing Mode | Syntax | Opcode | \# of bytes | \# of cycles |
| --- | --- | --- | --- | --- |
| Implied | SET | F4  | 1   | 2   |

_Flags Affected_

| N   | V   | T   | B   | D   | I   | Z   | C   |
| --- | --- | --- | --- | --- | --- | --- | --- |
| -   | -   | 1   | -   | -   | -   | -   | -   |

Store HuC6270 No. 0 (ST0)
-------------------------

_Function_ The immediate argument is stored in the HuC6270's address register. This command is equivalent to storing the immediate argument in \\$1FE000. The HuC6270 "No. 0" register is also known as the HuC6270 Address/Status Register; more information is available in the HuC6270 summary. According to the _Develo Book_ , this operation sets /CE7, A1, and A0 to logical LOW.

_Adressing Modes & Opcodes_

| Addressing Mode | Syntax | Opcode | \# of bytes | \# of cycles |
| --- | --- | --- | --- | --- |
| Implied | ST0 #nn | 03 nn | 2   | 4   |

_Flags Affected_

| N   | V   | T   | B   | D   | I   | Z   | C   |
| --- | --- | --- | --- | --- | --- | --- | --- |
| -   | -   | 0   | -   | -   | -   | -   | -   |

Store HuC6270 No. 1 (ST1)
-------------------------

_Function_ The immediate argument is stored in the HuC6270's low data register. This command is equivalent to storing the immediate argument in \\$1FE002. The HuC6270 "No. 1" register is also known as the HuC6270 Low Data Register; more information is available in the HuC6270 summary. According to the _Develo Book_ , this operation sets /CE7 and A0 to logical LOW, while setting A1 to logical HIGH.

_Adressing Modes & Opcodes_

| Addressing Mode | Syntax | Opcode | \# of bytes | \# of cycles |
| --- | --- | --- | --- | --- |
| Implied | ST1 #nn | 13 nn | 2   | 4   |

_Flags Affected_

| N   | V   | T   | B   | D   | I   | Z   | C   |
| --- | --- | --- | --- | --- | --- | --- | --- |
| -   | -   | 0   | -   | -   | -   | -   | -   |

Store HuC6270 No. 2 (ST2)
-------------------------

_Function_ The immediate argument is stored in the HuC6270's high data register. This command is equivalent to storing the immediate argument in \\$1FE003. The HuC6270 "No. 2" register is also known as the HuC6270 High Data Register; more information is available in the HuC6270 summary. According to the _Develo Book_ , this operation sets /CE7 to logical LOW, while setting A0 and A1 to logical HIGH.

_Adressing Modes & Opcodes_

| Addressing Mode | Syntax | Opcode | \# of bytes | \# of cycles |
| --- | --- | --- | --- | --- |
| Implied | ST2 #nn | 23 nn | 2   | 4   |

_Flags Affected_

| N   | V   | T   | B   | D   | I   | Z   | C   |
| --- | --- | --- | --- | --- | --- | --- | --- |
| -   | -   | 0   | -   | -   | -   | -   | -   |

Set Memory Bit i (SMBi)
-----------------------

_Function_ Set the specified bit in the zero page memory location specified in the operand. The bit to clear is specified by a number concatenated to the end of the mnemonic, resulting in 8 distinct Opcodes.

_Adressing Modes & Opcodes_

| Addressing Mode | Syntax | Opcode | \# of bytes | \# of cycles |
| --- | --- | --- | --- | --- |
| Zero page | SMB0 ZZ | 87 ZZ | 2   | 7   |
| Zero page | SMB1 ZZ | 97 ZZ | 2   | 7   |
| Zero page | SMB2 ZZ | A7 ZZ | 2   | 7   |
| Zero page | SMB3 ZZ | B7 ZZ | 2   | 7   |
| Zero page | SMB4 ZZ | C7 ZZ | 2   | 7   |
| Zero page | SMB5 ZZ | D7 ZZ | 2   | 7   |
| Zero page | SMB6 ZZ | E7 ZZ | 2   | 7   |
| Zero page | SMB7 ZZ | F7 ZZ | 2   | 7   |

_Flags Affected_

| N   | V   | T   | B   | D   | I   | Z   | C   |
| --- | --- | --- | --- | --- | --- | --- | --- |
| -   | -   | 0   | -   | -   | -   | -   | -   |

Store Accumulator to Memory (STA)
---------------------------------

_Function_ Stores the value in the accumulator to the effective address specified by the operand.

_Adressing Modes & Opcodes_

| Addressing Mode | Syntax | Opcode | \# of bytes | \# of cycles |
| --- | --- | --- | --- | --- |
| Zero Page | STA ZZ | 85 ZZ | 2   | 4   |
| Zero Page, X | STA ZZ, X | 95 ZZ | 2   | 4   |
| Indirect | STA (ZZ) | 92 ZZ | 2   | 7   |
| Indexed Indirect, X | STA (ZZ, X) | 81 ZZ | 2   | 7   |
| Indirect Indexed, Y | STA (ZZ), Y | 91 ZZ | 2   | 7   |
| Absolute | STA hhll | 8D ll hh | 3   | 5   |
| Absolute, X | STA hhll, X | 9D ll hh | 3   | 5   |
| Absolute, Y | STA hhll, Y | 99 ll hh | 3   | 5   |

_Flags Affected_

| N   | V   | T   | B   | D   | I   | Z   | C   |
| --- | --- | --- | --- | --- | --- | --- | --- |
| -   | -   | 0   | -   | -   | -   | -   | -   |

Store X Register to Memory (STX)
--------------------------------

_Function_ Store the value in the X register to the effective address specified by the operand.

_Adressing Modes & Opcodes_

| Addressing Mode | Syntax | Opcode | \# of bytes | \# of cycles |
| --- | --- | --- | --- | --- |
| Zero Page | STX ZZ | 86 ZZ | 2   | 4   |
| Zero Page, Y | STX ZZ, Y | 96 ZZ | 2   | 4   |
| Absolute | STX hhll | 8E ll hh | 3   | 5   |

_Flags Affected_

| N   | V   | T   | B   | D   | I   | Z   | C   |
| --- | --- | --- | --- | --- | --- | --- | --- |
| -   | -   | 0   | -   | -   | -   | -   | -   |

Store Y Register to Memory (STY)
--------------------------------

_Function_ Store the value in the Y register to the effective address specified by the operand.

_Adressing Modes & Opcodes_

| Addressing Mode | Syntax | Opcode | \# of bytes | \# of cycles |
| --- | --- | --- | --- | --- |
| Zero Page | STY ZZ | 84 ZZ | 2   | 4   |
| Zero Page, X | STY ZZ, X | 94 ZZ | 2   | 4   |
| Absolute | STY hhll | 8C ll hh | 3   | 5   |

_Flags Affected_

| N   | V   | T   | B   | D   | I   | Z   | C   |
| --- | --- | --- | --- | --- | --- | --- | --- |
| -   | -   | 0   | -   | -   | -   | -   | -   |

Store Zero to Memory (STZ)
--------------------------

_Function_ Store the value #\\$00 to the effective address specified by the operand. Very useful for initialising memory.

_Adressing Modes & Opcodes_

| Addressing Mode | Syntax | Opcode | \# of bytes | \# of cycles |
| --- | --- | --- | --- | --- |
| Zero Page | STZ ZZ | 64 ZZ | 2   | 4   |
| Zero Page, X | STZ ZZ, X | 74 ZZ | 2   | 4   |
| Absolute | STZ hhll | 9C ll hh | 3   | 5   |
| Absolute, X | STZ hhll, X | 9E ll hh | 3   | 5   |

_Flags Affected_

| N   | V   | T   | B   | D   | I   | Z   | C   |
| --- | --- | --- | --- | --- | --- | --- | --- |
| -   | -   | 0   | -   | -   | -   | -   | -   |

Transfer Alternate Increment (TAI)
----------------------------------

_Function_ Execute a memory move where the source address alternates between two addresses, and the destination address increments with each loop cycle. This is an extremely powerful instruction, mainly used for transferring data from the special video memory (e.g., backgrounds, etc.) to the main memory.

_Adressing Modes & Opcodes_

| Addressing Mode | Syntax | Opcode | \# of bytes | \# of cycles |
| --- | --- | --- | --- | --- |
| Block Move | TAI SHSL,DHDL, LHLL | F3 SL SH DL DH LL LH | 7   | 17 + 6x |

_Flags Affected_

| N   | V   | T   | B   | D   | I   | Z   | C   |
| --- | --- | --- | --- | --- | --- | --- | --- |
| -   | -   | 0   | -   | -   | -   | -   | -   |

Swap X and Y Registers (SXY)
----------------------------

_Function_ Swaps the values stored in the X and Y registers.

_Adressing Modes & Opcodes_

| Addressing Mode | Syntax | Opcode | \# of bytes | \# of cycles |
| --- | --- | --- | --- | --- |
| Implied | SXY | 02  | 1   | 3   |

_Flags Affected_

| N   | V   | T   | B   | D   | I   | Z   | C   |
| --- | --- | --- | --- | --- | --- | --- | --- |
| -   | -   | 0   | -   | -   | -   | -   | -   |

Transfer Accumulator to MPRi (TAMi)
-----------------------------------

_Function_ Loads Memory Mapping Register i with the value in the accumulator. More about the MPR registers can be found in the Memory Mapping summary. It is possible to load more than one MPR at a time by setting more than one bit in the immediate argument to TAM.

_Adressing Modes & Opcodes_

| Addressing Mode | Syntax | Opcode | \# of bytes | \# of cycles |
| --- | --- | --- | --- | --- |
| Implied | TAMi (TAM #nn) | 53 ($2^i$) | 2   | 5   |

_Flags Affected_

| N   | V   | T   | B   | D   | I   | Z   | C   |
| --- | --- | --- | --- | --- | --- | --- | --- |
| -   | -   | 0   | -   | -   | -   | -   | -   |

Transfer Accumulator to X Register (TAX)
----------------------------------------

_Function_ Transfer the value in the accumulator to register X.

_Adressing Modes & Opcodes_

| Addressing Mode | Syntax | Opcode | \# of bytes | \# of cycles |
| --- | --- | --- | --- | --- |
| Implied | TAX | AA  | 1   | 2   |

_Flags Affected_

| N   | V   | T   | B   | D   | I   | Z   | C   |
| --- | --- | --- | --- | --- | --- | --- | --- |
| N   | -   | 0   | -   | -   | -   | Z   | -   |

Transfer Accumulator to Y Register (TAY)
----------------------------------------

_Function_ Transfer the value in the accumulator to register Y.

_Adressing Modes & Opcodes_

| Addressing Mode | Syntax | Opcode | \# of bytes | \# of cycles |
| --- | --- | --- | --- | --- |
| Implied | TAY | A8  | 1   | 2   |

_Flags Affected_

| N   | V   | T   | B   | D   | I   | Z   | C   |
| --- | --- | --- | --- | --- | --- | --- | --- |
| N   | -   | 0   | -   | -   | -   | Z   | -   |

Transfer Increment Alternate (TIA)
----------------------------------

_Function_ Execute a memory move where the source address increments, and the destination address alternates between two addresses with each loop cycle. This is an extremely powerful instruction, mainly used for transferring data to the special video memory (e.g., backgrounds, etc.) from the main memory.

_Adressing Modes & Opcodes_

| Addressing Mode | Syntax | Opcode | \# of bytes | \# of cycles |
| --- | --- | --- | --- | --- |
| Block Move | TIA SHSL,DHDL, LHLL | E3 SL SH DL DH LL LH | 7   | 17 + 6x |

_Flags Affected_

| N   | V   | T   | B   | D   | I   | Z   | C   |
| --- | --- | --- | --- | --- | --- | --- | --- |
| -   | -   | 0   | -   | -   | -   | -   | -   |

Transfer Decrement Decrement (TDD)
----------------------------------

_Function_ Execute a memory move where the source and destination addresses decrement with each loop cycle. This is an extremely powerful instruction, mainly used for copying and moving data around in main memory.

_Adressing Modes & Opcodes_

| Addressing Mode | Syntax | Opcode | \# of bytes | \# of cycles |
| --- | --- | --- | --- | --- |
| Block Move | TDD SHSL,DHDL, LHLL | C3 SL SH DL DH LL LH | 7   | 17 + 6x |

_Flags Affected_

| N   | V   | T   | B   | D   | I   | Z   | C   |
| --- | --- | --- | --- | --- | --- | --- | --- |
| -   | -   | 0   | -   | -   | -   | -   | -   |

Transfer Increment None (TIN)
-----------------------------

_Function_ Execute a memory move where the source address increments with each loop cycle. This is an extremely powerful instruction, mainly used for transferring data from the special video memory (e.g., backgrounds, etc.) to the main memory.

_Adressing Modes & Opcodes_

| Addressing Mode | Syntax | Opcode | \# of bytes | \# of cycles |
| --- | --- | --- | --- | --- |
| Block Move | TIN SHSL,DHDL, LHLL | D3 SL SH DL DH LL LH | 7   | 17 + 6x |

_Flags Affected_

| N   | V   | T   | B   | D   | I   | Z   | C   |
| --- | --- | --- | --- | --- | --- | --- | --- |
| -   | -   | 0   | -   | -   | -   | -   | -   |

Transfer Increment Increment (TII)
----------------------------------

_Function_ Execute a memory move where the source and destination addresses increment with each loop cycle. This is an extremely powerful instruction, mainly used for copying and moving blocks of data around in main memory.

_Adressing Modes & Opcodes_

| Addressing Mode | Syntax | Opcode | \# of bytes | \# of cycles |
| --- | --- | --- | --- | --- |
| Block Move | TII SHSL,DHDL, LHLL | 73 SL SH DL DH LL LH | 7   | 17 + 6x |

_Flags Affected_

| N   | V   | T   | B   | D   | I   | Z   | C   |
| --- | --- | --- | --- | --- | --- | --- | --- |
| -   | -   | 0   | -   | -   | -   | -   | -   |

Transfer MPRi to Accumulator (TMAi)
-----------------------------------

_Function_ Transfers the value in Memory Mapping Register i to the accumulator. More information about the MPRs can be found on the Memory Mapping summary. Only one bit in the immediate argument can be set to 1.

_Adressing Modes & Opcodes_

| Addressing Mode | Syntax | Opcode | \# of bytes | \# of cycles |
| --- | --- | --- | --- | --- |
| Implied | TMAi (TMA #nn) | 43 ($2^i$) | 2   | 4   |

_Flags Affected_

| N   | V   | T   | B   | D   | I   | Z   | C   |
| --- | --- | --- | --- | --- | --- | --- | --- |
| -   | -   | 0   | -   | -   | -   | -   | -   |

Test and Reset Memory Bits Against Accumulator (TRB)
----------------------------------------------------

_Function_ Logically AND together the _complement_ of the value in the accumulator with the data at the effective address specified by the operand. Store the result at the memory location. This clears each bit for which the corresponding accumulator bit is set, making it an ideal opcode for masking data. N and V and Z are set as in the BIT opcode instruction. These flags are set based on the ANDing of the _uncomplemented_ accumulator value with the memory value.

_Adressing Modes & Opcodes_

| Addressing Mode | Syntax | Opcode | \# of bytes | \# of cycles |
| --- | --- | --- | --- | --- |
| Zero Page | TRB ZZ | 14 ZZ | 2   | 6   |
| Absolute | TRB hhll | 1C ll hh | 3   | 7   |

_Flags Affected_

| N   | V   | T   | B   | D   | I   | Z   | C   |
| --- | --- | --- | --- | --- | --- | --- | --- |
| M7  | M6  | 0   | -   | -   | -   | Z   | -   |

Test and Set Memory Bits Against Accumulator (TSB)
--------------------------------------------------

_Function_ Logically OR together the value in the accumulator with the data at the effective address specified by the operand. Store the result at the memory location. This sets each bit for which the corresponding accumulator bit is set, making it an ideal opcode for masking data. N and V and Z are set as in the BIT opcode instruction. These flags are set based on the ANDing of the accumulator value with the memory value.

_Adressing Modes & Opcodes_

| Addressing Mode | Syntax | Opcode | \# of bytes | \# of cycles |
| --- | --- | --- | --- | --- |
| Zero Page | TSB ZZ | 04 ZZ | 2   | 6   |
| Absolute | TSB hhll | 0C ll hh | 3   | 7   |

_Flags Affected_

| N   | V   | T   | B   | D   | I   | Z   | C   |
| --- | --- | --- | --- | --- | --- | --- | --- |
| M7  | M6  | 0   | -   | -   | -   | Z   | -   |

Test and Reset Memory Bits (TST)
--------------------------------

_Function_ Logically AND together the immediate operand with the data at the effective address specified by the operand. This sets each bit for which the corresponding immediate argument bit is set, making it an ideal opcode for masking data. N and V and Z are set as in the BIT opcode instruction.

_Adressing Modes & Opcodes_

| Addressing Mode | Syntax | Opcode | \# of bytes | \# of cycles |
| --- | --- | --- | --- | --- |
| Imm. Zero Page | TST #nn, ZZ | 83 nn ZZ | 3   | 7   |
| Imm. Zero Page, X | TST #nn, ZZ, X | A3 nn ZZ | 3   | 7   |
| Immediate Absolute | TST #nn, hhll | 93 nn ll hh | 4   | 8   |
| Imm. Absolute, X | TST #nn, hhll, X | B3 nn ll hh | 4   | 8   |

_Flags Affected_

| N   | V   | T   | B   | D   | I   | Z   | C   |
| --- | --- | --- | --- | --- | --- | --- | --- |
| M7  | M6  | 0   | -   | -   | -   | Z   | -   |

Transfer Stack Pointer to X Register (TSX)
------------------------------------------

_Function_ Transfer the value in the stack pointer S to the X register. The value of the stack pointer is not changed.

_Adressing Modes & Opcodes_

| Addressing Mode | Syntax | Opcode | \# of bytes | \# of cycles |
| --- | --- | --- | --- | --- |
| Implied | TSX | BA  | 1   | 2   |

_Flags Affected_

| N   | V   | T   | B   | D   | I   | Z   | C   |
| --- | --- | --- | --- | --- | --- | --- | --- |
| N   | -   | 0   | -   | -   | -   | Z   | -   |

Transfer X Register to Accumulator (TXA)
----------------------------------------

_Function_ Transfer the value in the X register to the accumulator. The value of the X register is not changed.

_Adressing Modes & Opcodes_

| Addressing Mode | Syntax | Opcode | \# of bytes | \# of cycles |
| --- | --- | --- | --- | --- |
| Implied | TXA | 8A  | 1   | 2   |

_Flags Affected_

| N   | V   | T   | B   | D   | I   | Z   | C   |
| --- | --- | --- | --- | --- | --- | --- | --- |
| N   | -   | 0   | -   | -   | -   | Z   | -   |

_Function_ Transfer the value in the Y register to the accumulator. The value of the Y register is not changed.

_Adressing Modes & Opcodes_

| Addressing Mode | Syntax | Opcode | \# of bytes | \# of cycles |
| --- | --- | --- | --- | --- |
| Implied | TYA | 98  | 1   | 2   |

_Flags Affected_

| N   | V   | T   | B   | D   | I   | Z   | C   |
| --- | --- | --- | --- | --- | --- | --- | --- |
| N   | -   | 0   | -   | -   | -   | Z   | -   |

Transfer X Register to Stack Pointer (TXS)
------------------------------------------

_Function_ Transfer the value in the X register to the stack pointer. The value of the X register is not changed.

_Adressing Modes & Opcodes_

| Addressing Mode | Syntax | Opcode | \# of bytes | \# of cycles |
| --- | --- | --- | --- | --- |
| Implied | TXS | 9A  | 1   | 2   |

_Flags Affected_

| N   | V   | T   | B   | D   | I   | Z   | C   |
| --- | --- | --- | --- | --- | --- | --- | --- |
| -   | -   | 0   | -   | -   | -   | -   | -   |