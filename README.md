# verilog-fundamentals
# Verilog Study Notes

This repository contains study notes on **basic Verilog syntax**, abstraction levels, lexical tokens, identifiers, white space, number literals, keywords, and data types.  
It is written as a learning reference with **explanations and example codes**.

---

## Table of Contents
1. Abstraction Levels
2. Lexical Tokens
3. Identifier Rules
4. White Space
5. Numbers
6. Hexadecimal Conversion Table
7. Verilog Keywords
8. Verilog Data Types & Logic Values

---

## 1. Abstraction Levels

Digital design can be described at **four abstraction levels**:

| Level | Description | Example |
|-------|-------------|---------|
| Switch Level | Transistor-level design (MOSFET) | CMOS Inverter |
| Gate Level   | Logic gates (AND, OR, XOR …) | Half Adder |
| RTL (Register Transfer Level) | Register-to-register data transfer with operations (synthesizable) | D-FF |
| Algorithmic Level | High-level algorithms, later refined to RTL | Factorial |

### Switch Level Example
```verilog
module inverter (out, in);
  input in; output out;
  supply1 vdd; supply0 gnd;
  pmos p1(out, vdd, in);
  nmos n1(out, gnd, in);
endmodule
Gate Level Example
verilog
코드 복사
module half_adder (sum, carry, a, b);
  input a, b; output sum, carry;
  xor (sum, a, b);
  and (carry, a, b);
endmodule
RTL Example
verilog
코드 복사
module dff (q, d, clk);
  input d, clk; output reg q;
  always @(posedge clk) q <= d;
endmodule
Algorithmic Example
verilog
코드 복사
module factorial #(parameter N=5) (result);
  output reg [31:0] result; integer i;
  initial begin
    result = 1;
    for (i = 1; i <= N; i = i + 1)
      result = result * i;
  end
endmodule
2. Lexical Tokens
A Verilog program is composed of tokens:

Keywords: module, endmodule, always, if … (reserved words)

Identifiers: user-defined names (signals, modules, variables)

Operators: + - * / && || ! == …

Numbers: 3'b001, 5'd30, 16'hABCD …

Strings: "Hello"

Comments:

Single-line: //

Multi-line: /* ... */

3. Identifier Rules
Identifiers = names you define for variables, signals, modules, etc.

Rules:

Must start with a letter (a–z, A–Z) or underscore _

Invalid: 1var

Valid: var1, _temp, data123

After the first character, you may use letters, digits, _, $

Example: count_1, data$bus, fifo_rd0

$ can appear in the middle or end, but cannot be the first character

Valid: data$1, signal$bus

Invalid: $data, $temp

Case-sensitive

DATA, data, Data are all different identifiers

Reserved keywords cannot be used as identifiers

Example: module, wire, always

verilog
코드 복사
reg data1;       // valid
reg _counter;    // valid
reg value$next;  // valid
reg $value;      // invalid
reg 1value;      // invalid
4. White Space
Spaces, tabs, and newlines are only token separators

Multiple whitespaces are ignored

Semicolons (;) end statements, not line breaks

For macros (define), use \ to continue a line

verilog
코드 복사
assign sum = a +
             b;   // line break allowed, semicolon ends the statement
5. Numbers
General format:

php-template
코드 복사
[<size>]'[<radix>]<value>
Size = number of bits

Radix:

b = binary

o = octal

d = decimal

h = hexadecimal

Value = actual number (hex uses 0–9, A–F)

Examples:

3'b001 → 3-bit binary 001 = decimal 1

5'd30 → 5-bit decimal 30 = binary 11110

16'h5ED4 → 16-bit hex 5ED4 = binary 0101 1110 1101 0100 = decimal 24276

16'hABCD → 16-bit hex ABCD = binary 1010 1011 1100 1101 = decimal 43981

6. Hexadecimal Conversion Table
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

7. Verilog Keywords (Reserved Words)
Verilog has a set of reserved keywords which cannot be used as identifiers.

Module & Structure
module, endmodule, primitive, endprimitive, macromodule

Data Types
wire, reg, tri, tri0, tri1, triand, trior, trireg

supply0, supply1

integer, real, time, realtime

parameter, localparam

Procedural Blocks
initial, always

Control Flow
begin, end, if, else

case, endcase

for, while, repeat, forever

disable

Timing & Event Control
posedge, negedge, wait

Operators
and, or, xor, xnor, not, nand, nor

Tasks & Functions
task, endtask, function, endfunction

Generate
generate, endgenerate

Miscellaneous
assign, deassign, force, release

specify, endspecify

specparam, defparam

event, genvar

System Tasks (start with $)
$display, $monitor, $finish, $stop

$time, $realtime, $random

$dumpvars, $dumpoff, $dumpfile

Identifiers cannot start with $ (reserved for system tasks).
Keywords are case-sensitive: module ≠ Module.

8. Verilog Data Types & Logic Values
Verilog supports multiple data types for modeling hardware:

Net Types
wire – represents physical connections, driven continuously

tri, tri0, tri1 – like wire, with default values

supply0, supply1 – constant 0 or 1 (power/ground modeling)

Register Types
reg – holds value until reassigned (not necessarily a hardware register)

integer, time, real, realtime – simulation-only data types

Parameters
parameter, localparam – constants, often used for configuration

Logic Values
Verilog is a 4-valued logic system:

Value	Meaning
0	Logic zero / Low
1	Logic one / High
x	Unknown (could be 0 or 1, simulation uncertainty)
z	High impedance (disconnected / floating wire)

Examples:

verilog
코드 복사
reg a = 1'b0;   // logic 0
reg b = 1'b1;   // logic 1
reg c = 1'bx;   // unknown
reg d = 1'bz;   // high impedance
Summary
Abstraction Levels: Switch → Gate → RTL → Algorithmic

Lexical Tokens: keywords, identifiers, operators, numbers, strings, comments

Identifiers: must start with letter/underscore, case-sensitive, $ not first

White Space: ignored except as token separators; semicolon ends statements

Numbers: [size]'[radix][value], supports binary/octal/decimal/hex

Hex Table: quick conversion between hex, binary, decimal

Keywords: reserved words (cannot be identifiers)

Data Types: wire, reg, integer, parameter, etc.

Logic Values: 0, 1, x, z
