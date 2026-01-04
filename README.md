BC Language Guide (v0.2.6), 
Note: Install MinGW to compile .bc files into .exe. Total commands: 69

[Include File]
#include "file" - Import another file (supports nesting).

[Integer Operations]
SET/GET/ADD/SUB/MUL/DIV/CLR/CLRA/INC/DEC/MOV/SWP/CMP/POW/ABS/RAND - Standard math and memory operations.

[Logic & Comparisons (v0.2.6)]
IFLV/IFBV target - Jump if memory[addr] is Less (<) or Bigger (>) than value.
IFLEV/IFBEV target - Jump if memory[addr] is Less or Equal (<=) or Bigger or Equal (>=) than value.
IFLA/IFBA target - Jump if memory[addr1] < or > memory[addr2].
IFLEA/IFBEA target - Jump if memory[addr1] <= or >= memory[addr2].

[Control Flow & Functions]
LBL name - Create a label.
JMP line/label - Direct jump.
CALL name / RET - Function call system with stack.
JZ/JNZ addr.target - Jump if zero / not zero.
IFV/IFNV addr.val.target - Jump if equal / not equal to value.
IFA/IFNA addr1.addr2.target - Jump if memory values are equal / not equal.

[File System]
OPEN "path",mode,data - Modes: R (read), W (write), WA (write addr), A (append).
FCHK "path",saddr - Check file existence.

[String Operations]
SSET/SGET/SINP/SCLR/SCLRA/SMOV/SSWP/SCMP/SSETM/SIFV/SIFA/SIFNV/SIFNA.

[System]
PRT/PRTL "text" - Output.
CLS - Clear screen.
DUMP - Show memory.
PAS - Pause.
HLT - Terminate.
