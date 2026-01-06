╔════════════════════════════════════════════════════════════════════════════╗
║                    BC LANGUAGE - COMPLETE GUIDE (v0.2.9)                   ║
╚════════════════════════════════════════════════════════════════════════════╝

REQUIREMENTS:
- Install MinGW (g++ compiler) to compile .bc files into .exe
- Total commands: 77
- Memory: 1024 float cells (0-1023) + 1024 string cells (0-1023)

═══════════════════════════════════════════════════════════════════════════
[1] INCLUDE FILES
═══════════════════════════════════════════════════════════════════════════
#include "filename.bc"
  - Import another .bc file into current program
  - Supports nested includes
  - Example:
    #include "math_lib.bc"
    #include "utils.bc"

═══════════════════════════════════════════════════════════════════════════
[2] FLOAT MEMORY OPERATIONS
═══════════════════════════════════════════════════════════════════════════

SET addr.value
  - Set float value to memory address
  - Example: SET 0.42.5  (memory[0] = 42.5)

GET addr
  - Print value from memory address
  - Example: GET 0  (prints memory[0])

INP addr
  - Get float input from user
  - Example: INP 5  (user types number → memory[5])

CLR addr
  - Clear memory address (set to 0)
  - Example: CLR 10

CLRA
  - Clear ALL memory addresses (0-1023)
  - Example: CLRA

INC addr
  - Increment value by 1
  - Example: INC 0  (memory[0]++)

DEC addr
  - Decrement value by 1
  - Example: DEC 0  (memory[0]--)

MOV src.dest
  - Copy value from src to dest
  - Example: MOV 0.1  (memory[1] = memory[0])

SWP addr1.addr2
  - Swap two memory values
  - Example: SWP 0.1  (swap memory[0] ↔ memory[1])

CMP addr1.addr2
  - Compare two addresses, prints 1 if equal, 0 if not
  - Example: CMP 0.1

DUMP [start[.end]]
  - Print memory contents
  - DUMP - prints all (0-1023)
  - DUMP 10 - prints from address 10 to end (10-1023)
  - DUMP 0.10 - prints range (0-10)
  - Example: 
    DUMP       : shows all memory
    DUMP 5     : shows memory[5] to memory[1023]
    DUMP 0.5   : shows memory[0] to memory[5]

═══════════════════════════════════════════════════════════════════════════
[3] MATHEMATICAL OPERATIONS
═══════════════════════════════════════════════════════════════════════════

ADD addr1.addr2.result
  - result = addr1 + addr2
  - Example: ADD 0.1.2  (memory[2] = memory[0] + memory[1])

SUB addr1.addr2.result
  - result = addr1 - addr2
  - Example: SUB 5.3.7

MUL addr1.addr2.result
  - result = addr1 * addr2
  - Example: MUL 0.1.2

DIV addr1.addr2.result
  - result = addr1 / addr2
  - Division by zero is ignored (result unchanged)
  - Example: DIV 10.2.5

POW base.exponent.result
  - result = base ^ exponent
  - Example: POW 2.3.0  (memory[0] = 2^3 = 8)

ABS addr.result
  - result = absolute value of addr
  - Example: ABS 5.6

RAND min.max.result
  - Generate random integer between min and max
  - Example: RAND 1.100.0  (memory[0] = random 1-100)

═══════════════════════════════════════════════════════════════════════════
[4] RANGE OPERATIONS
═══════════════════════════════════════════════════════════════════════════

SETM start.end.value
  - Set range of addresses to value
  - Example: SETM 0.10.5  (memory[0-10] = 5)

MOVM start.end.source
  - Copy value from source to range
  - Example: MOVM 0.5.10  (memory[0-5] = memory[10])

CLRM start.end
  - Clear range of addresses
  - Example: CLRM 0.100

GETM start.end
  - Print range of memory values
  - Example: GETM 0.5

═══════════════════════════════════════════════════════════════════════════
[5] CONTROL FLOW & JUMPS
═══════════════════════════════════════════════════════════════════════════

JMP line
  - Unconditional jump to LINE NUMBER ONLY
  - Cannot jump to labels, only to line numbers
  - Example: JMP 10

JZ addr.line
  - Jump to LINE NUMBER if memory[addr] == 0
  - Example: JZ 0.25

JNZ addr.line
  - Jump to LINE NUMBER if memory[addr] != 0
  - Example: JNZ 5.30

IMPORTANT: JMP, JZ, JNZ can ONLY jump to line numbers, NOT to labels!

═══════════════════════════════════════════════════════════════════════════
[6] CONDITIONAL JUMPS - VALUE COMPARISON
═══════════════════════════════════════════════════════════════════════════

IFV addr.value.target
  - Jump to LINE NUMBER or LABEL if memory[addr] == value
  - Example: 
    IFV 0.42.10      : jump to line 10
    IFV 0.42.success : jump to label "success"

IFNV addr.value.target
  - Jump to LINE NUMBER or LABEL if memory[addr] != value
  - Example: IFNV 0.0.not_zero

IFLV addr.value.target
  - Jump to LINE NUMBER or LABEL if memory[addr] < value
  - Example: IFLV 0.10.less_than_ten

IFBV addr.value.target
  - Jump to LINE NUMBER or LABEL if memory[addr] > value
  - Example: IFBV 0.100.greater

IFLEV addr.value.target
  - Jump to LINE NUMBER or LABEL if memory[addr] <= value
  - Example: IFLEV 0.50.check

IFBEV addr.value.target
  - Jump to LINE NUMBER or LABEL if memory[addr] >= value
  - Example: IFBEV 0.18.adult

═══════════════════════════════════════════════════════════════════════════
[7] CONDITIONAL JUMPS - ADDRESS COMPARISON
═══════════════════════════════════════════════════════════════════════════

IFA addr1.addr2.target
  - Jump to LINE NUMBER or LABEL if memory[addr1] == memory[addr2]
  - Example: IFA 0.1.equal

IFNA addr1.addr2.target
  - Jump to LINE NUMBER or LABEL if memory[addr1] != memory[addr2]
  - Example: IFNA 0.1.not_equal

IFLA addr1.addr2.target
  - Jump to LINE NUMBER or LABEL if memory[addr1] < memory[addr2]
  - Example: IFLA 5.10.first_smaller

IFBA addr1.addr2.target
  - Jump to LINE NUMBER or LABEL if memory[addr1] > memory[addr2]
  - Example: IFBA 20.10.first_bigger

IFLEA addr1.addr2.target
  - Jump to LINE NUMBER or LABEL if memory[addr1] <= memory[addr2]
  - Example: IFLEA 0.100.within_range

IFBEA addr1.addr2.target
  - Jump to LINE NUMBER or LABEL if memory[addr1] >= memory[addr2]
  - Example: IFBEA 18.0.valid

═══════════════════════════════════════════════════════════════════════════
[8] FUNCTIONS
═══════════════════════════════════════════════════════════════════════════

LBL name
  - Create a label (function entry point)
  - MUST always end with RET
  - Example:
    LBL main
        PRTL "Hello"
    RET

CALL label
  - Call function by LABEL NAME (pushes return address to stack)
  - Can ONLY call labels, NOT line numbers
  - Example: CALL print_hello

RET
  - Return from function (pops return address from stack)
  - MUST be at end of EVERY LBL block
  - Example:
    LBL my_function
        PRTL "Inside function"
    RET

IMPORTANT RULES:
  - Functions MUST be called with CALL, NOT JMP
  - Every LBL MUST end with RET
  - CALL works only with label names
  - JMP works only with line numbers

Full Example:
  CALL greet
  HLT
  
  LBL greet
      PRTL "Hello, World!"
  RET

═══════════════════════════════════════════════════════════════════════════
[9] STRING OPERATIONS
═══════════════════════════════════════════════════════════════════════════

SSET addr.text
  - Set string value at address
  - Example: SSET 0.Hello World

SGET addr
  - Print string from address
  - Example: SGET 0

SINP addr
  - Get string input from user
  - Example: SINP 1

SCLR addr
  - Clear string at address
  - Example: SCLR 0

SCLRA
  - Clear all string memory
  - Example: SCLRA

SMOV src.dest
  - Copy string from src to dest
  - Example: SMOV 0.1

SSWP addr1.addr2
  - Swap two strings
  - Example: SSWP 0.1

SCMP addr1.addr2
  - Compare strings, prints 1 if equal, 0 if not
  - Example: SCMP 0.1

SDUMP [start[.end]]
  - Print string memory contents
  - SDUMP - prints all (0-1023)
  - SDUMP 10 - prints from address 10 to end (10-1023)
  - SDUMP 0.10 - prints range (0-10)
  - Example:
    SDUMP      : shows all string memory
    SDUMP 5    : shows string[5] to string[1023]
    SDUMP 0.5  : shows string[0] to string[5]

═══════════════════════════════════════════════════════════════════════════
[10] STRING RANGE OPERATIONS
═══════════════════════════════════════════════════════════════════════════

SSETM start.end.text
  - Fill range with text
  - Example: SSETM 0.5.Empty

SMOVM start.end.source
  - Copy string from source to range
  - Example: SMOVM 0.10.5

SCLRM start.end
  - Clear string range
  - Example: SCLRM 0.100

SGETM start.end
  - Print string range
  - Example: SGETM 0.5

═══════════════════════════════════════════════════════════════════════════
[11] STRING CONDITIONAL JUMPS
═══════════════════════════════════════════════════════════════════════════

SIFV addr.value.target
  - Jump to LINE NUMBER or LABEL if string[addr] == "value"
  - Example: SIFV 0.yes.confirmed

SIFNV addr.value.target
  - Jump to LINE NUMBER or LABEL if string[addr] != "value"
  - Example: SIFNV 0.exit.continue

SIFA addr1.addr2.target
  - Jump to LINE NUMBER or LABEL if string[addr1] == string[addr2]
  - Example: SIFA 0.1.match

SIFNA addr1.addr2.target
  - Jump to LINE NUMBER or LABEL if string[addr1] != string[addr2]
  - Example: SIFNA 0.1.different

═══════════════════════════════════════════════════════════════════════════
[12] TYPE CONVERSION
═══════════════════════════════════════════════════════════════════════════

CHR code_addr.str_addr
  - Convert ASCII code to character
  - Example:
    SET 0.65           : ASCII code for 'A'
    CHR 0.1            : string[1] = "A"
    SGET 1             : prints "A"

STF str_addr.float_addr
  - Convert string to float
  - If conversion fails, result = 0
  - Example:
    SSET 0.123.45
    STF 0.1            : memory[1] = 123.45
    GET 1              : prints 123.45

FTS str_addr.float_addr
  - Convert float to string
  - Example:
    SET 0.42.5
    FTS 1.0            : string[1] = "42.5"
    SGET 1             : prints "42.5"

═══════════════════════════════════════════════════════════════════════════
[13] OUTPUT
═══════════════════════════════════════════════════════════════════════════

PRT "text"
  - Print text without newline
  - Example: PRT "Hello "

PRTL "text"
  - Print text with newline
  - Example: PRTL "Hello World"

ENDL
  - Print empty line (newline only)
  - Example: ENDL

═══════════════════════════════════════════════════════════════════════════
[14] KEYBOARD INPUT
═══════════════════════════════════════════════════════════════════════════

GK addr
  - Get single key press (no echo)
  - Stores ASCII code in memory[addr]
  - Example:
    PRTL "Press any key..."
    GK 0               : waits for key press
    GET 0              : shows ASCII code
    CHR 0.1            : convert to character
    SGET 1             : display character

═══════════════════════════════════════════════════════════════════════════
[15] FILE OPERATIONS
═══════════════════════════════════════════════════════════════════════════

OPEN "path",mode,data

Modes:
  R   - Read file into string memory
        OPEN "data.txt",R,0  (reads into string[0])
  
  W   - Write literal text to file
        OPEN "out.txt",W,Hello World
  
  WA  - Write from string address to file
        OPEN "out.txt",WA,0  (writes string[0] to file)
  
  A   - Append literal text to file
        OPEN "log.txt",A,New entry

Examples:
  : Read file
  OPEN "config.txt",R,5
  SGET 5
  
  : Write to file
  SSET 0.Important data
  OPEN "save.txt",WA,0
  
  : Append log
  OPEN "log.txt",A,Program started

═══════════════════════════════════════════════════════════════════════════
[16] SYSTEM COMMANDS
═══════════════════════════════════════════════════════════════════════════

CLS
  - Clear console screen
  - Example: CLS

SYS "command"
  - Execute system command
  - Windows: SYS "dir"
  - Linux: SYS "ls"
  - Example:
    SYS "echo Hello"
    SYS "mkdir test"
    SYS "notepad.exe"

PAS
  - Pause and wait for key press
  - Example: PAS

HLT
  - Terminate program immediately
  - Example: HLT

═══════════════════════════════════════════════════════════════════════════
[17] TIME & DELAY
═══════════════════════════════════════════════════════════════════════════

SLP addr
  - Sleep for milliseconds (value from memory[addr])
  - Example:
    SET 0.1000         : 1000 ms = 1 second
    SLP 0              : wait 1 second

GT millis_addr.time_str_addr
  - Get current time
  - memory[millis_addr] = milliseconds since epoch
  - string[time_str_addr] = "HH:MM:SS" format
  - Example:
    GT 0.1
    GET 0              : prints timestamp
    SGET 1             : prints "14:30:45"

═══════════════════════════════════════════════════════════════════════════
[18] COMMENTS
═══════════════════════════════════════════════════════════════════════════

: comment text :
  - Single or multi-line comments
  - Example:
    : This is a comment :
    SET 0.10 : set value : GET 0

═══════════════════════════════════════════════════════════════════════════
[19] COMPLETE EXAMPLES
═══════════════════════════════════════════════════════════════════════════

─────────────────────────────────────────────────────────────────────────
EXAMPLE 1: Hello World
─────────────────────────────────────────────────────────────────────────
PRTL "Hello, World!"
HLT

─────────────────────────────────────────────────────────────────────────
EXAMPLE 2: Simple Calculator
─────────────────────────────────────────────────────────────────────────
PRTL "Enter first number:"
INP 0
PRTL "Enter second number:"
INP 1
ADD 0.1.2
PRT "Result: "
GET 2
HLT

─────────────────────────────────────────────────────────────────────────
EXAMPLE 3: Loop Example (Count to 10) - Using Line Numbers
─────────────────────────────────────────────────────────────────────────
SET 0.0
GET 0
ENDL
INC 0
IFLV 0.10.2
HLT

─────────────────────────────────────────────────────────────────────────
EXAMPLE 4: Loop Example (Count to 10) - Using Labels
─────────────────────────────────────────────────────────────────────────
SET 0.0
LBL loop
    GET 0
    ENDL
    INC 0
    IFLV 0.10.loop
RET

─────────────────────────────────────────────────────────────────────────
EXAMPLE 5: Function Call (CORRECT WAY)
─────────────────────────────────────────────────────────────────────────
CALL greet
CALL greet
HLT

LBL greet
    PRTL "Hello from function!"
RET

─────────────────────────────────────────────────────────────────────────
EXAMPLE 6: Menu System - Using CALL for Functions
─────────────────────────────────────────────────────────────────────────
CALL menu
HLT

LBL menu
    CLS
    PRTL "1. Start"
    PRTL "2. Exit"
    PRT "Choice: "
    INP 0
    IFV 0.1.start
    IFV 0.2.exit
    CALL menu
RET

LBL start
    PRTL "Starting..."
    SET 0.1000
    SLP 0
    CALL menu
RET

LBL exit
    PRTL "Goodbye!"
RET

─────────────────────────────────────────────────────────────────────────
EXAMPLE 7: Key Press Detection
─────────────────────────────────────────────────────────────────────────
CALL main
HLT

LBL main
    PRTL "Press ESC to exit"
    CALL wait_key
RET

LBL wait_key
    GK 0
    CHR 0.1
    PRT "You pressed: "
    SGET 1
    ENDL
    IFNV 0.27.wait_key  : 27 = ESC key
    PRTL "Exiting..."
RET

─────────────────────────────────────────────────────────────────────────
EXAMPLE 8: File Logger
─────────────────────────────────────────────────────────────────────────
GT 0.1
SSET 2.Log entry: 
OPEN "log.txt",A,Log entry: 
OPEN "log.txt",WA,1
OPEN "log.txt",A,\n
PRTL "Log saved!"
HLT

─────────────────────────────────────────────────────────────────────────
EXAMPLE 9: Random Number Game - Using CALL
─────────────────────────────────────────────────────────────────────────
CALL main
HLT

LBL main
    RAND 1.10.0
    PRTL "Guess number (1-10):"
    CALL guess_loop
RET

LBL guess_loop
    INP 1
    IFA 0.1.win
    IFLA 1.0.too_low
    PRTL "Too high! Try again:"
    CALL guess_loop
RET

LBL too_low
    PRTL "Too low! Try again:"
    CALL guess_loop
RET

LBL win
    PRTL "You win!"
RET

─────────────────────────────────────────────────────────────────────────
EXAMPLE 10: Memory Dump Test
─────────────────────────────────────────────────────────────────────────
: Fill some memory
SETM 0.5.100
SET 10.999
SET 20.777

PRTL "Full dump:"
DUMP

PRTL "From address 10 onwards:"
DUMP 10

PRTL "Range 0-20:"
DUMP 0.20
HLT

─────────────────────────────────────────────────────────────────────────
EXAMPLE 11: Type Conversion Demo
─────────────────────────────────────────────────────────────────────────
: Number to string
SET 0.123.45
FTS 1.0
PRT "Float as string: "
SGET 1
ENDL

: String to number
SSET 2.999.99
STF 2.3
PRT "String as float: "
GET 3
ENDL

: ASCII to character
SET 4.72
SET 5.105
CHR 4.6
CHR 5.7
PRT "Characters: "
SGET 6
SGET 7
ENDL
HLT

═══════════════════════════════════════════════════════════════════════════
[20] TIPS & BEST PRACTICES
═══════════════════════════════════════════════════════════════════════════

1. Memory Management:
   - Use addresses 0-99 for temporary variables
   - Use 100-999 for arrays/large data
   - Reserve specific ranges for different purposes

2. Function Organization:
   - Put all LBL definitions at the end of file
   - ALWAYS end functions with RET
   - Use CALL at the start, then HLT before first LBL
   - NEVER use JMP to call functions - use CALL only

3. Code Structure (CORRECT):
   CALL main
   HLT
   
   LBL main
       : your code here
   RET
   
   LBL other_function
       : ...
   RET

4. Jump Rules (IMPORTANT):
   - JMP, JZ, JNZ → Can ONLY jump to LINE NUMBERS
   - CALL → Can ONLY call LABEL NAMES
   - IF* commands → Can jump to BOTH line numbers AND labels
   - Every LBL MUST end with RET

5. Error Prevention:
   - Always check division by zero before DIV
   - Validate user input with conditional jumps
   - Clear memory before reusing addresses
   - Never forget RET at end of LBL blocks

6. Performance:
   - Use range operations (SETM, CLRM) for bulk changes
   - Minimize file operations in loops
   - Use functions to avoid code duplication

7. Debugging:
   - Use DUMP to inspect memory state
   - Use SDUMP to inspect string memory
   - Add PRTL messages to trace execution flow
   - Use PAS to pause at critical points

8. File Operations:
   - Always check if file operations succeed
   - Use WA mode to write dynamic content
   - Close files properly by ending program or using new OPEN

9. String Handling:
   - Remember string memory is separate from float memory
   - Use CHR for character manipulation
   - Use STF/FTS for conversions between types

10. Common Mistakes to Avoid:
    - Using JMP to call functions (use CALL instead)
    - Forgetting RET at end of LBL
    - Trying to JMP to a label (use line numbers or IF* commands)
    - Trying to CALL a line number (use label names only)

═══════════════════════════════════════════════════════════════════════════

For more info and updates, visit: [your website/repo]
Report bugs: [your contact]

═══════════════════════════════════════════════════════════════════════════
