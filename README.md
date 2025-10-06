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
Nets vs. variables

wire (a net)

Does not store a value. It just reflects whatever its drivers are doing.

Must be driven continuously (e.g., by assign, a module port, or a primitive).

Example: assign y = a & b; // y must be a net (default wire).

reg (a variable)

Stores the last value assigned in a procedural block (always, initial).

Not driven by assign.

Default width is 1 bit unless you declare a vector: reg [7:0] r;

Ports: input, output, inout — wire or reg?

In classic Verilog (1995/2001):

input: must be a net (defaults to wire). You can’t write input reg (that’s illegal in Verilog; it’s allowed only in SystemVerilog with logic).

output: can be a net or a reg.

Use output reg if you assign it inside an always/initial.

Use plain output (wire) if you drive it with a continuous assignment or by connecting through.

inout: must be a net (tri-state bus), i.e., a wire (often tri). Not a reg.

Quick examples:

module m(
  input       a,            // wire by default
  input [3:0] b,            // wire [3:0]
  output      y,            // wire (must be driven by assign or instance)
  output reg  q,            // reg (driven in always)
  inout       sda           // wire/tri (tri-stated somewhere)
);
  assign y = a & b[0];      // ok: y is a wire
  always @* q = a ^ b[1];   // ok: q is a reg
endmodule

assign vs. procedural assignment

assign → continuous, for nets (wire).
Example: assign sum = x + y;

Procedural =/<= inside always/initial → for regs.
Example:

always @(posedge clk) q <= d;

integer type

integer in Verilog is a 32-bit signed variable (4-state).

Good for loop indices, counters in testbenches, file I/O, etc.

It’s a variable like reg but fixed width = 32 bits and signed.

Other built-ins: time (64-bit unsigned), real (double), etc.

Sizing constants (avoid accidental truncation/sign issues)

Unsized literals default to 32-bit and may sign-extend if used in signed contexts.

Best practice: size your literals to the signal width you mean.

8'd255, 12'hABC, 1'b0, 1'b1

If a variable “holds constants,” declare it with the minimum needed width and use sized constants to match:

reg [3:0] nibble = 4'd10;     // sized literal matches width
wire [1:0] sel   = 2'b01;


For parameters:

parameter WIDTH = 12;
localparam [WIDTH-1:0] MASK = {WIDTH{1'b1}}; // width-safe


In SystemVerilog, prefer logic for ports/regs and use $bits(signal) or int'(expr) casts to size/convert cleanly:

logic [7:0] a = 8'(5);     // sized cast

Common gotchas to remember

Driving a wire inside always → illegal.

Driving a reg with assign → illegal.

Leaving a wire undriven → it floats to z, not a stored value.

Declaring input reg (pure Verilog) → illegal (use input wire or just input; or use SystemVerilog logic).

upply0 and supply1

These are special net types in Verilog that are permanently tied to logic 0 and 1.

supply0 = logic 0 (ground, GND)

supply1 = logic 1 (power, VDD)

They’re stronger than wire or reg — like hardwired constants.

Example:
module supply_example(output wire a, output wire b);

  // declare nets
  supply0 gnd;   // always 0
  supply1 vdd;   // always 1

  // connect them
  assign a = gnd; // a is tied to 0
  assign b = vdd; // b is tied to 1

endmodule


In hardware this models a pin connected straight to GND or VDD.

2. parameter and parameter [range]

A parameter is a constant you can set inside a module.
You can make it a scalar, a vector (with [range]), or give it a value.

Example (scalar parameter):
module param_ex1;
  parameter WIDTH = 8;          // scalar constant
  reg [WIDTH-1:0] data;         // uses WIDTH to size reg
endmodule

Example (vector parameter):
module param_ex2;
  parameter [7:0] INIT_VAL = 8'hA5; // 8-bit parameter with default value
  reg [7:0] r = INIT_VAL;           // initialize register with parameter
endmodule


Here:

parameter [7:0] INIT_VAL means "this parameter is 8 bits wide."

Its default value is 8'hA5 (hex A5 = 1010_0101).

When you instantiate, you can override the parameter:

param_ex2 #(.INIT_VAL(8'hFF)) u1();  // now INIT_VAL = 11111111

✅ Putting both together
module top;
  supply0 GND;      // tied to logic 0
  supply1 VDD;      // tied to logic 1

  parameter [7:0] CONST = 8'd63;  // 8-bit constant

  wire [7:0] sig0, sig1;

  assign sig0 = {8{GND}};   // sig0 = 00000000
  assign sig1 = CONST & {8{VDD}}; // sig1 = CONST (since VDD = 1s)

endmodule
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
