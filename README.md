BC Language Guide (v0.2.5),
Note: Install MinGW to compile .bc files into .exe Total commands: 61

[Include File]
#include "file" - Import another file ".bc or .bh" (supports nesting and quotes).

[Integer Operations]
SET addr.value - Set integer (0-1023) to address.

GET addr - Print integer value from address.

ADD/SUB/MUL/DIV addr1.addr2 - Mathematical operations.

CLR addr / CLRA - Clear value at address or all integer memory.

INC addr / DEC addr - Increment (+1) and decrement (-1).

MOV addr1.addr2 - Copy value from addr1 to addr2.

SWP addr1.addr2 - Swap values between two addresses.

CMP addr1.addr2 - Compare (print 1 if equal, else 0).

POW addr1.addr2.addr3 - Power (addr3 = addr1 ^ addr2).

ABS addr1.addr2 - Get absolute value of addr1 and save to addr2.

RAND min.max.addr - Generate random number into address.

[File System]
OPEN "path",R,saddr - Read file content into string memory.

OPEN "path",W,"text" - Write text directly to file (quotes are trimmed).

OPEN "path",WA,saddr - Write string memory data to file.

OPEN "path",A,"text" - Append text to the end of a file.

FCHK "path",saddr - Check if file exists (saves "true"/"false" to smemory).

[Output & System]
PRT "text" - Print text to console.

PRTL "text" - Print text and move to a new line.

DUMP - Show all memory (also DUMP addr or DUMP a1.a2).

INP addr - Input integer from user to address.

PAS - Pause the program (wait for key press).

[Control Flow & Functions]
LBL name - Create a label (registered in lbls).

JMP line/label - Jump to a specific line number or label name.

CALL name - Execute function by label.

RET - Return from function.

JZ/JNZ addr.target - Jump if value is zero / NOT zero.

IFV/IFNV addr.value.target - Jump if value equals/not equals constant (target = line or label).

IFA/IFNA addr1.addr2.target - Jump if addr1 value equals/not equals addr2 value.

[String Memory Operations]
SSET saddr.value - Set string value (supports quotes).

SGET saddr - Print string value from s-address.

SINP saddr - Input string from user to s-address.

SCLR/SCLRA - Clear string at s-address or all string memory.

SMOV/SSWP - Copy or swap string values.

SCMP s1.s2 - Compare two strings (1 if equal, 0 if not).

SIFV saddr.value.target - Jump if string equals constant.

SIFA s1.s2.target - Jump if s-string1 equals s-string2.

SIFNV/SIFNA ... - Conditional jumps for "NOT equal".

[Terminal Command]
HLT - End of the program (terminate execution).
