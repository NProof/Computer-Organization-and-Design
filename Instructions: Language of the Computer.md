### Index

* [Introduction](#introduction)
* [Operatrions of the Computer Hardware](#operatrions_of_the_computer_hardware)
* [Operands of ths Computer Hardware](#operands_of_ths_computer_hardware)
* [Representing Instructions in the Computer](#representing_instructions_in_the_computer)
* [Logical Opertions](#logical_operations)
* [Instructions for Making Decisions](#instructions_for_making_decisions)
* [Supportiong Procedures in Computer Hardware](#supporting_procedures_in_computer_hardware)
* [Communicating with People](#communicating_with_people)
* [MIPS Addressing for 32-Bits Immediates and Addresses](#mips_addressing_for_32-bit_immediates_and_addresses)
* [Fallacies and Pitfalls](#fallacies_and_pitfalls)

### Introduction

* To command a computer's hardware
  * Instructions: ths words of a Computer's language
  * Instruction set: vocabulary of a computer's language
* Computer languages are quite similar
  * All computers are constrcted from hardware technolgies based on similar underlying principles
  * There are a few basic operations that all computers must provide
  * A common goal for computer designers
    * To find a language that makes it easy to build the hardware and the compiler
    * To maximize performance and minimize cost and energy
  * MIPS instruction set
  * Stored-program concept
    * instuctions and data of many types can be stored in memory as numbers
    
### Operatrions_of_the_Computer_Hardware
#### MIPS arithmetic instruction
* add/sub a,b,c

#### MIPS operands
* 32 registers
  * $s0-$s7, $t0-$t9, $zero, $a0-$a3, $v0-$v1, $gp, $fp, $sp, $ra, $at  
  $zero always equals 0  
  register $at is reserved by the assembler to handle large constants.
* 2<sup>30</sup> momery words
  * Memory[0], Memory[4], ... , Memory[4294967292]   
  Accessed only by transfer instructions. MIPS uses byte addreese. so sequential word addresses differ by 4. Memory holds data structures, arrays, and spilled registers.
* ![id](http://www.jamalalsakran.me/Org/MIPS.jpg)
* Design principle 1: simplicity favors regularity

### Operands_of_ths_Computer_Hardware
* Variables vs. operands
  * Unlike programs in high-level languages, the operands of arithmetic instructions are <a alt = "受限制的">restricted</a>
    * Operands must be from a limited number of special locations called registers
    * MIPS has 32 32-bit registers (1 word = 32 bits)
    * Typically 32 registers on current computers
  * Design principle 2: smaller is faster
    * Larger number of registers may increase the clock cycle time and the number of bits required in the instruction format
    * To balance between the designer’s desire and the limitation of hardware
  * Example: f = (g + h) – (i + j);
    * (f, g, h, i, j) are in ($s0, $s1, $s2, $s3, $s4)
    * add	$t0, $s1, $s2  
    add	$t1, $s3, $s4  
    sub	$s0, $t0, $t1
* Memory operands
  * Registers only keep small amount of data, but memory contains millions of data elements
    * Memory is a large single-dimensional array
    * Address acts as the index to the memory, starting at 0
  * Data transfer instructions
    * lw	$destination, offset($base)
    * sw	$source, offset($base)
  * Memory address = contents of the base register + offset
    * Base register: the second register of the instruction
    * Offset: the constant portion of the instruction
* Constant or immediate operands

### Representing_Instructions_in_the_Computer
* MIPS Fields  
[//]: # ( ![](http://slideplayer.com/slide/5018290/16/images/5/MIPS+Instruction+Formats.jpg) )
![](http://slideplayer.com/slide/5018290/16/images/6/MIPS+R-Type+(ALU)+Instruction+Fields.jpg)
* Design principle 3: Good design demands good compromises
  * To keep all instructions the same length, thereby requiring more than one instruction formats
![](http://player.slideplayer.com/13/3741739/data/images/img49.jpg)
* Store-program concept
  * Key principles
     * Instructions are represented as numbers
     * Programs are stored in memory to be read or written, just like data
  * Fetch and execute cycle
     * Instructions are fetched and put into a special register
     * Bits in the register control the subsequent actions
     * Fetch the next instruction and continue
### Logical_Operations
* sll
* srl
* R-format instructions
  * shamt
* and, andi
* or, ori
* nor, nori

### Instructions_for_Making_Decisions
* beq
* bne
* j
* basic block
  * A sequence of instructions without branches (except possibly at the end) and without branch targets or branch labels (except possibly at the beginning)
  * One of the first early phase of compilation is breaking the program into basic blocks
* Set on less than instruction
  * slt
  * slti
  * sltu = Set on less than unsigned
  * sltiu = Set on less than immediate unsigned
* Case/switch statement
  * Jump address table (jump table)
  * Jump register (jr)

### Supporting_Procedures_in_Computer_Hardware

#### Using more registers
```
int leaf_example (int g, int h, int i, int j)  
{  
   int f;  
   f = (g + h) – (i + j);  
   return f;  
}  
```
```mips
(f, g, h, i, j) are in ($s0, $a0, $a1, $a2, $a3)

leaf_example:	addi	$sp, $sp, -12	# adjust stack to make room for 3 items
	sw	$t1, 8($sp)	# save $t1 for use afterwards
	sw	$t0, 4($sp)	# save $t0 for use afterwards
	sw	$s0, 0($sp)	# save $s0 for use afterwards
	add	$t0, $a0, $a1	# $t0 contains g + h
	add	$t1, $a2, $a3	# $t1 contains i + j
	sub	$s0, $t0, $t1	# f = $t0 - $t1, which is (g + h) – (i + j)
	add	$v0, $s0, $zero	# returns f ($v0 = $s0 + 0)
	lw	$s0, 0($sp)	# restore $s0 for caller
	lw	$t0, 4($sp)	# restore $t0 for caller
	lw	$t1, 8($sp)	# restore $t1 for caller
	addi	$sp, $sp, 12	# adjust stack to delete 3 items
	jr	$ra	# jump back to calling routine
```
### Communicating_with_People
### MIPS_Addressing_for_32-bit_Immediates_and_Addresses
##### Addressing in branches and jumps
##### MIPS addressing mode summary

### Fallacies_and_Pitfalls
##### Fallacies
##### Pitfalls
