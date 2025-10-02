# verilog-fundarmentals
#  Verilog Study Notes

This repository contains study notes on **basic Verilog syntax**, abstraction levels, lexical tokens, identifiers, white space, and number literals.  
It is written as a learning reference with **explanations + example codes**.

---

##  Table of Contents
1. Abstraction Levels
2. Lexical Tokens
3. Identifier Rules
4. White Space
5. Numbers
6. Hexadecimal Conversion Table

---

## 1️ Abstraction Levels

Digital design can be described at **four abstraction levels**:

| Level | Description | Example |
|-------|-------------|---------|
| **Switch Level** | Transistor-level design (MOSFET) | CMOS Inverter |
| **Gate Level**   | Logic gates (AND, OR, XOR …) | Half Adder |
| **RTL (Register Transfer Level)** | Register-to-register data transfer with operations (synthesizable) | D-FF |
| **Algorithmic Level** | High-level algorithms, later refined to RTL | Factorial |

###  Switch Level Example
```verilog
module inverter (out, in);
  input in; output out;
  supply1 vdd; supply0 gnd;
  pmos p1(out, vdd, in);
  nmos n1(out, gnd, in);
endmodule
 Gate Level Example
verilog
code
module half_adder (sum, carry, a, b);
  input a, b; output sum, carry;
  xor (sum, a, b);
  and (carry, a, b);
endmodule
 RTL Example
verilog
code
module dff (q, d, clk);
  input d, clk; output reg q;
  always @(posedge clk) q <= d;
endmodule
 Algorithmic Example
verilog
code
module factorial #(parameter N=5) (result);
  output reg [31:0] result; integer i;
  initial begin
    result = 1;
    for (i = 1; i <= N; i = i + 1)
      result = result * i;
  end
endmodule
2️⃣ Lexical Tokens
A Verilog program is composed of tokens:

Keywords: module, endmodule, always, if … (reserved words)

Identifiers: user-defined names (signals, modules, variables)

Operators: + - * / && || ! == …

Numbers: 3'b001, 5'd30, 16'hABCD …

Strings: "Hello"

Comments:

Single-line: //

Multi-line: /* ... */

3️⃣ Identifier Rules
Identifiers = names you define for variables, signals, modules, etc.

 Rules
Must start with a letter (a–z, A–Z) or underscore _

X 1var (invalid)

✅ var1, _temp, data123 (valid)

After the first character, you may use letters, digits, _, $

Example: count_1, data$bus, fifo_rd0

$ can appear in the middle or end, but cannot be the first character

✅ data$1, signal$bus

❌ $data, $temp

Case-sensitive

DATA, data, Data are all different identifiers

Reserved keywords cannot be used as identifiers

Example: module, wire, always are invalid as names

verilog
code
reg data1;       // valid
reg _counter;    // valid
reg value$next;  // valid
reg $value;      // invalid
reg 1value;      // invalid
4️⃣ White Space
Spaces, tabs, and newlines are only token separators

Multiple whitespaces are ignored

Semicolons (;) end statements, not line breaks

For macros (define), use \ to continue a line

verilog
code
assign sum = a +
             b;   // line break allowed, semicolon ends the statement
5️⃣ Numbers
General format:

php-template
code
[<size>]'[<radix>]<value>
Size = number of bits

Radix:

b = binary

o = octal

d = decimal

h = hexadecimal

Value = actual number (hex uses 0–9, A–F)

 Examples
3'b001 → 3-bit binary 001 = decimal 1

5'd30 → 5-bit decimal 30 = binary 11110

16'h5ED4 → 16-bit hex 5ED4 = binary 0101 1110 1101 0100 = decimal 24276

16'hABCD → 16-bit hex ABCD = binary 1010 1011 1100 1101 = decimal 43981

6️⃣ Hexadecimal Conversion Table
Hex	Binary	Decimal
0	0000	0
1	0001	1
2	0010	2
3	0011	3
4	0100	4
5	0101	5
6	0110	6
7	0111	7
8	1000	8
9	1001	9
A	1010	10
B	1011	11
C	1100	12
D	1101	13
E	1110	14
F	1111	15
7 Verilog Keywords (Reserved Words)

Verilog has a set of keywords that are reserved — you cannot use them as identifiers (variable names, module names, etc.).

Here’s a categorized list:

🔹 Module & Structure

module, endmodule

primitive, endprimitive

macromodule

🔹 Data Types

wire, reg, tri, tri0, tri1, triand, trior, trireg

supply0, supply1

integer, real, time, realtime

parameter, localparam

🔹 Procedural Blocks

initial, always

🔹 Control Flow

begin, end

if, else

case, endcase

for, while, repeat, forever

disable

🔹 Timing & Event Control

# (delay operator, not a keyword but syntax)

@ (event control)

posedge, negedge

wait

🔹 Operators (keywords-like)

and, or, xor, xnor, not, nand, nor

🔹 Tasks & Functions

task, endtask

function, endfunction

🔹 Generate

generate, endgenerate

🔹 Miscellaneous

assign, deassign, force, release

specify, endspecify

specparam

defparam

event

genvar

🔹 System Tasks (start with $)

These are not keywords in the strict sense, but built-in system tasks:

$display, $monitor, $finish, $stop

$time, $realtime, $random

$dumpvars, $dumpoff, $dumpfile

⚠️ Important: You cannot use $ at the beginning of an identifier → reserved for system tasks.

✅ Key Notes

Keywords are case-sensitive → Module ≠ module.

Cannot be used as identifiers (e.g., reg module; ❌).

System tasks always start with $.
 Summary
Abstraction levels: Switch → Gate → RTL → Algorithmic

Lexical Tokens: smallest language units (keywords, identifiers, operators, numbers …)

Identifiers: must start with letter/underscore, $ not allowed as first char, case-sensitive

White Space: ignored except as token separators; semicolon ends a statement

Numbers: [size]'[radix][value], supports binary/octal/decimal/hex; A–F = 10–15 in hex
