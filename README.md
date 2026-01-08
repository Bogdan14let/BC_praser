╔═══════════════════════════════════════════════════════════════════════════╗
║                    BC LANGUAGE - COMPLETE GUIDE (v0.3.1)                  ║
╚═══════════════════════════════════════════════════════════════════════════╝

REQUIREMENTS:
- Install MinGW (g++ compiler) to compile .bc files into .exe
- Total commands: 77
- Memory: 1024 float cells (0-1023) + 1024 string cells (0-1023)
- Named variables support: unlimited float/string variables with names

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
[2] VARIABLES - NEW FEATURE! 🎉
═══════════════════════════════════════════════════════════════════════════

BC Language now supports NAMED VARIABLES in addition to numbered addresses!

You can use either:
  - Numbered addresses: 0, 1, 2, ..., 1023
  - Named variables: myVar, counter, userName, etc.

Named variables automatically:
  - Become LOCAL inside functions (after LBL)
  - Become GLOBAL in main code (before any LBL)
  - Are isolated between function calls

Examples:
  SET counter.0          : named variable 'counter' = 0
  SET 0.42               : address 0 = 42 (old style still works)
  INC counter            : counter++
  GET counter            : print counter value
  
  SSET userName.Alice    : string variable 'userName' = "Alice"
  SGET userName          : print "Alice"

Variable Scope Rules:
  - Variables created in MAIN code → GLOBAL (accessible everywhere)
  - Variables created in FUNCTIONS → LOCAL (only in that function)
  - Function parameters are always LOCAL
  - Numbered addresses (0-1023) are GLOBAL everywhere

═══════════════════════════════════════════════════════════════════════════
[3] FLOAT MEMORY OPERATIONS (Works with BOTH addresses and names)
═══════════════════════════════════════════════════════════════════════════

SET target.value
  - Set float value to memory address OR variable name
  - Example: 
    SET 0.42.5           : memory[0] = 42.5
    SET counter.100      : counter = 100
    SET myVar.3.14       : myVar = 3.14

GET target
  - Print value from memory address OR variable
  - Example: 
    GET 0                : print memory[0]
    GET counter          : print counter variable

INP target
  - Get float input from user into address OR variable
  - Example: 
    INP 5                : user types → memory[5]
    INP userAge          : user types → userAge variable

CLR target
  - Clear memory address OR variable (set to 0)
  - Example: 
    CLR 10               : memory[10] = 0
    CLR counter          : counter = 0

CLRA
  - Clear ALL memory addresses AND variables
  - Example: CLRA

INC target
  - Increment address OR variable by 1
  - Example: 
    INC 0                : memory[0]++
    INC counter          : counter++

DEC target
  - Decrement address OR variable by 1
  - Example: 
    DEC 0                : memory[0]--
    DEC lives            : lives--

MOV src.dest
  - Copy value from src to dest (both can be addresses or names)
  - Example: 
    MOV 0.1              : memory[1] = memory[0]
    MOV counter.backup   : backup = counter
    MOV score.0          : memory[0] = score

SWP target1.target2
  - Swap two memory values (addresses or names)
  - Example: 
    SWP 0.1              : swap memory[0] ↔ memory[1]
    SWP x.y              : swap x ↔ y

CMP target1.target2
  - Compare two values, prints 1 if equal, 0 if not
  - Example: 
    CMP 0.1              : compare addresses
    CMP score.highScore  : compare variables

DUMP [start[.end]]
  - Print memory contents AND variable values
  - DUMP - prints all (0-1023) + global vars + local vars
  - DUMP 10 - prints from address 10 to end
  - DUMP 0.10 - prints range (0-10)
  - Example: 
    DUMP       : shows all memory + all variables
    DUMP 5     : shows memory[5-1023]
    DUMP 0.5   : shows memory[0-5]

═══════════════════════════════════════════════════════════════════════════
[4] MATHEMATICAL OPERATIONS (Works with addresses AND variables)
═══════════════════════════════════════════════════════════════════════════

ADD target1.target2.result
  - result = target1 + target2 (any can be address or variable)
  - Example: 
    ADD 0.1.2            : memory[2] = memory[0] + memory[1]
    ADD score.bonus.total : total = score + bonus
    ADD x.5.result       : result = x + memory[5]

SUB target1.target2.result
  - result = target1 - target2
  - Example: 
    SUB 5.3.7            : memory[7] = memory[5] - memory[3]
    SUB health.damage.newHealth : newHealth = health - damage

MUL target1.target2.result
  - result = target1 * target2
  - Example: 
    MUL 0.1.2            : memory[2] = memory[0] * memory[1]
    MUL price.quantity.total : total = price * quantity

DIV target1.target2.result
  - result = target1 / target2
  - Division by zero returns 0
  - Example: 
    DIV 10.2.5           : memory[5] = memory[10] / memory[2]
    DIV total.count.average : average = total / count

POW base.exponent.result
  - result = base ^ exponent
  - Example: 
    POW 2.3.0            : memory[0] = 2^3 = 8
    POW base.exp.power   : power = base^exp

ABS target.result
  - result = absolute value of target
  - Example: 
    ABS 5.6              : memory[6] = abs(memory[5])
    ABS temperature.absTemp : absTemp = abs(temperature)

RAND min.max.result
  - Generate random integer between min and max
  - Example: 
    RAND 1.100.0         : memory[0] = random 1-100
    RAND 1.6.diceRoll    : diceRoll = random 1-6

═══════════════════════════════════════════════════════════════════════════
[5] RANGE OPERATIONS (Only for numbered addresses 0-1023)
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
[6] CONTROL FLOW & JUMPS
═══════════════════════════════════════════════════════════════════════════

JMP line
  - Unconditional jump to LINE NUMBER ONLY
  - Cannot jump to labels, only to line numbers
  - Example: JMP 10

JZ target.line
  - Jump to LINE NUMBER if target == 0 (address or variable)
  - Example: 
    JZ 0.25              : jump to line 25 if memory[0] == 0
    JZ counter.30        : jump to line 30 if counter == 0

JNZ target.line
  - Jump to LINE NUMBER if target != 0
  - Example: 
    JNZ 5.30             : jump if memory[5] != 0
    JNZ lives.10         : jump if lives != 0

IMPORTANT: JMP, JZ, JNZ can ONLY jump to line numbers, NOT to labels!

═══════════════════════════════════════════════════════════════════════════
[7] CONDITIONAL JUMPS - VALUE COMPARISON (Works with variables!)
═══════════════════════════════════════════════════════════════════════════

IFV target.value.destination
  - Jump to LINE NUMBER or LABEL if target == value
  - Example: 
    IFV 0.42.10          : jump to line 10
    IFV score.100.win    : jump to label "win"
    IFV choice.1.option1 : jump if choice == 1

IFNV target.value.destination
  - Jump if target != value
  - Example: IFNV lives.0.alive

IFLV target.value.destination
  - Jump if target < value
  - Example: IFLV age.18.minor

IFBV target.value.destination
  - Jump if target > value
  - Example: IFBV score.100.highScore

IFLEV target.value.destination
  - Jump if target <= value
  - Example: IFLEV health.20.danger

IFBEV target.value.destination
  - Jump if target >= value
  - Example: IFBEV level.10.expert

═══════════════════════════════════════════════════════════════════════════
[8] CONDITIONAL JUMPS - COMPARING TWO TARGETS (Variables supported!)
═══════════════════════════════════════════════════════════════════════════

IFA target1.target2.destination
  - Jump if target1 == target2
  - Example: 
    IFA 0.1.equal        : compare addresses
    IFA userPass.correctPass.login : compare variables

IFNA target1.target2.destination
  - Jump if target1 != target2
  - Example: IFNA player1.player2.different

IFLA target1.target2.destination
  - Jump if target1 < target2
  - Example: IFLA score.highScore.notBest

IFBA target1.target2.destination
  - Jump if target1 > target2
  - Example: IFBA score.highScore.newRecord

IFLEA target1.target2.destination
  - Jump if target1 <= target2
  - Example: IFLEA health.maxHealth.safe

IFBEA target1.target2.destination
  - Jump if target1 >= target2
  - Example: IFBEA level.requiredLevel.unlocked

═══════════════════════════════════════════════════════════════════════════
[9] FUNCTIONS - NOW WITH PARAMETERS! 🚀
═══════════════════════════════════════════════════════════════════════════

LBL name
LBL name(type param1, type param2, ...)
  - Create a function (label)
  - Can have parameters: fl (float) or str (string)
  - Parameters become LOCAL variables inside function
  - MUST always end with RET

Examples:
  : Simple function without parameters
  LBL greet
      PRTL "Hello!"
  RET

  : Function with float parameters
  LBL add(fl a, fl b)
      ADD a.b.result
      GET result
  RET

  : Function with mixed parameters
  LBL displayScore(str name, fl score)
      PRT "Player: "
      SGET name
      PRT " Score: "
      GET score
      ENDL
  RET

CALL label
CALL label(arg1, arg2, ...)
  - Call function by LABEL NAME
  - Pass arguments if function has parameters
  - Arguments can be addresses, variables, or literals

Examples:
  : Call without arguments
  CALL greet

  : Call with arguments
  SET score.100
  CALL add(50, score)          : passes 50 and score value
  
  SSET playerName.Alice
  CALL displayScore(playerName, score)

RET
  - Return from function
  - Automatically clears LOCAL variables
  - MUST be at end of EVERY LBL block

IMPORTANT RULES:
  - Functions create ISOLATED scope for local variables
  - Parameters are always LOCAL to the function
  - Global variables can be accessed from functions
  - Each function call gets fresh local variables

Full Example:
  : Main code
  SET x.10
  SET y.20
  CALL sum(x, y)
  HLT
  
  : Function adds two numbers
  LBL sum(fl a, fl b)
      ADD a.b.result     : result is LOCAL
      PRT "Sum = "
      GET result
      ENDL
  RET

═══════════════════════════════════════════════════════════════════════════
[10] STRING OPERATIONS (Works with addresses AND variables!)
═══════════════════════════════════════════════════════════════════════════

SSET target.text
  - Set string value (address or variable)
  - Example: 
    SSET 0.Hello World   : string[0] = "Hello World"
    SSET userName.Bob    : userName = "Bob"

SGET target
  - Print string
  - Example: 
    SGET 0               : print string[0]
    SGET userName        : print userName

SINP target
  - Get string input from user
  - Example: 
    SINP 1               : input → string[1]
    SINP userName        : input → userName

SCLR target
  - Clear string
  - Example: 
    SCLR 0               : string[0] = ""
    SCLR message         : message = ""

SCLRA
  - Clear all string memory AND string variables
  - Example: SCLRA

SMOV src.dest
  - Copy string from src to dest
  - Example: 
    SMOV 0.1             : string[1] = string[0]
    SMOV name.backup     : backup = name

SSWP target1.target2
  - Swap two strings
  - Example: 
    SSWP 0.1             : swap strings
    SSWP firstName.lastName : swap variables

SCMP target1.target2
  - Compare strings, prints 1 if equal, 0 if not
  - Example: 
    SCMP 0.1
    SCMP userInput.correctAnswer

SDUMP [start[.end]]
  - Print string memory + string variables
  - SDUMP - prints all (0-1023) + global + local string vars
  - SDUMP 10 - prints from address 10 to end
  - SDUMP 0.10 - prints range (0-10)

═══════════════════════════════════════════════════════════════════════════
[11] STRING RANGE OPERATIONS (Only for numbered addresses)
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
[12] STRING CONDITIONAL JUMPS (Works with variables!)
═══════════════════════════════════════════════════════════════════════════

SIFV target.value.destination
  - Jump if string target == "value"
  - Example: 
    SIFV 0.yes.confirmed
    SIFV answer.quit.exit

SIFNV target.value.destination
  - Jump if string target != "value"
  - Example: SIFNV command.exit.continue

SIFA target1.target2.destination
  - Jump if string target1 == string target2
  - Example: 
    SIFA 0.1.match
    SIFA password.correctPass.login

SIFNA target1.target2.destination
  - Jump if string target1 != string target2
  - Example: SIFNA input.expected.retry

═══════════════════════════════════════════════════════════════════════════
[13] TYPE CONVERSION (Works with variables!)
═══════════════════════════════════════════════════════════════════════════

CHR code_target.str_target
  - Convert ASCII code to character
  - Example:
    SET code.65          : ASCII 'A'
    CHR code.letter      : letter = "A"
    SGET letter          : prints "A"

STF str_target.float_target
  - Convert string to float
  - Returns 0 if conversion fails
  - Example:
    SSET input.123.45
    STF input.number     : number = 123.45
    GET number

FTS float_target.str_target
  - Convert float to string
  - Example:
    SET value.42.5
    FTS value.text       : text = "42.5"
    SGET text

═══════════════════════════════════════════════════════════════════════════
[14] OUTPUT
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
[15] KEYBOARD INPUT (Works with variables!)
═══════════════════════════════════════════════════════════════════════════

GK target
  - Get single key press (no echo)
  - Stores ASCII code in target
  - Example:
    GK keyCode           : wait for key
    GET keyCode          : show ASCII
    CHR keyCode.keyChar  : convert to char
    SGET keyChar         : display char

═══════════════════════════════════════════════════════════════════════════
[16] FILE OPERATIONS (Works with variables!)
═══════════════════════════════════════════════════════════════════════════

OPEN "path",mode,target

Modes:
  R   - Read file into string
        OPEN "data.txt",R,fileContent
  
  W   - Write literal text to file
        OPEN "out.txt",W,Hello World
  
  WA  - Write from string target to file
        OPEN "out.txt",WA,fileContent
  
  A   - Append literal text to file
        OPEN "log.txt",A,New entry

Examples:
  : Read file
  OPEN "config.txt",R,config
  SGET config
  
  : Write variable to file
  SSET data.Important info
  OPEN "save.txt",WA,data

═══════════════════════════════════════════════════════════════════════════
[17] SYSTEM COMMANDS
═══════════════════════════════════════════════════════════════════════════

CLS
  - Clear console screen

SYS "command"
  - Execute system command
  - Example: SYS "dir"

PAS
  - Pause and wait for key press

HLT
  - Terminate program immediately

═══════════════════════════════════════════════════════════════════════════
[18] TIME & DELAY (Works with variables!)
═══════════════════════════════════════════════════════════════════════════

SLP target
  - Sleep for milliseconds (from target)
  - Example:
    SET delay.1000       : 1 second
    SLP delay

GT millis_target.time_str_target
  - Get current time
  - millis_target = milliseconds since epoch
  - time_str_target = "HH:MM:SS"
  - Example:
    GT timestamp.timeString
    GET timestamp
    SGET timeString

═══════════════════════════════════════════════════════════════════════════
[19] COMMENTS
═══════════════════════════════════════════════════════════════════════════

: comment text :
  - Single or multi-line comments
  - Example:
    : This is a comment :
    SET counter.10 : initialize : GET counter

═══════════════════════════════════════════════════════════════════════════
[20] NEW EXAMPLES WITH VARIABLES & FUNCTIONS
═══════════════════════════════════════════════════════════════════════════

─────────────────────────────────────────────────────────────────────────
EXAMPLE 1: Variables Demo
─────────────────────────────────────────────────────────────────────────
SET counter.0
SET max.10

LBL loop
    GET counter
    ENDL
    INC counter
    IFLA counter.max.loop
RET

─────────────────────────────────────────────────────────────────────────
EXAMPLE 2: Function with Parameters
─────────────────────────────────────────────────────────────────────────
CALL greet(Alice, 25)
CALL greet(Bob, 30)
HLT

LBL greet(str name, fl age)
    PRT "Hello, "
    SGET name
    PRT "! You are "
    GET age
    PRTL " years old."
RET

─────────────────────────────────────────────────────────────────────────
EXAMPLE 3: Calculator with Named Variables
─────────────────────────────────────────────────────────────────────────
PRTL "Enter first number:"
INP num1
PRTL "Enter second number:"
INP num2

ADD num1.num2.sum
SUB num1.num2.diff
MUL num1.num2.prod
DIV num1.num2.quot

PRT "Sum: "
GET sum
ENDL
PRT "Difference: "
GET diff
ENDL
PRT "Product: "
GET prod
ENDL
PRT "Quotient: "
GET quot
ENDL
HLT

─────────────────────────────────────────────────────────────────────────
EXAMPLE 4: Local vs Global Variables
─────────────────────────────────────────────────────────────────────────
: Global variable
SET globalVar.100

CALL testScope
GET globalVar      : still 100 (global)
HLT

LBL testScope
    : Local variable
    SET localVar.50
    GET localVar   : prints 50
    GET globalVar  : prints 100 (can access global)
RET

─────────────────────────────────────────────────────────────────────────
EXAMPLE 5: Recursive Function (Countdown)
─────────────────────────────────────────────────────────────────────────
CALL countdown(10)
HLT

LBL countdown(fl n)
    IFLEV n.0.done
    GET n
    ENDL
    SUB n.1.next
    CALL countdown(next)
    LBL done
RET

─────────────────────────────────────────────────────────────────────────
EXAMPLE 6: String Variables in Functions
─────────────────────────────────────────────────────────────────────────
SSET message.Hello World
CALL printTwice(message)
HLT

LBL printTwice(str text)
    SGET text
    ENDL
    SGET text
    ENDL
RET

═══════════════════════════════════════════════════════════════════════════
[21] TIPS & BEST PRACTICES
═══════════════════════════════════════════════════════════════════════════

1. Variable Naming:
   - Use descriptive names: counter, playerName, highScore
   - Avoid single letters except for loops: i, j, x, y
   - CamelCase or snake_case both work

2. Memory Management:
   - Named variables: unlimited, auto-managed
   - Numbered addresses: use 0-1023 for legacy code or arrays
   - Functions get fresh local scope each call

3. Function Design:
   - Use parameters instead of global variables when possible
   - Keep functions small and focused
   - Always end with RET
   - Use descriptive function names

4. Scope Best Practices:
   - Declare globals at top of main code
   - Use locals inside functions for temporary data
   - Pass data via parameters, not globals

5. Type Safety:
   - fl parameters: for numbers
   - str parameters: for text
   - Use CHR, STF, FTS for conversions

═══════════════════════════════════════════════════════════════════════════

Version: v0.3.1-functions
New Features: Named variables, Function parameters, True function calls
Compiler: g++ with -std=c++17

═══════════════════════════════════════════════════════════════════════════
