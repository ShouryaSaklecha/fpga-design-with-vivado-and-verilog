# Verilog Fundamentals


## Identifiers
- Must always start with an alphabet
- Allowed to use numbers
- Can also use _
- **Case Sensitive**

```
module a_2 ; // valid
wire 3_fc; // invalid 

```
## Registers and Wire
Essentially the main building block of verilog HDL.
### Register
- Generally implements a register
- Not strictly defined as it is used everywhere
- They usually have a history (i.e, the property to store data)
- Used in procedural assignments. In procedural assignments, the LHS will always be a reg type.

### Wire
- Implies a connection
- Does not have a history
- Used in a continuous assignment where LHS will always be a wire.

```
reg a_1; // reg of 1 bit
reg [3:0] a_4; // a 4 bit reg
wire a; // one bit wire
wire [15:0] a_16; // a 16 bit bit wire
```
## Number Formats
Assume:
```
 reg[3:0] a;
```
You can specify numbers in a multiuple formats:
```
// format: SIZE RADIX VALUE;
reg[3:0] a = 4'd12; // creates a 4 bit value of decimal 12
reg[3:0] a = 4'b1100; // creates a 4 bit value of binary 12
reg[3:0] a = 4'o14; // creates a 4 bit value of octal 12
reg[3:0] a = 4'hc; // creates a 4 bit value of hexa 12
```
## Datatypes
### Synthesizable Datatypes
- **Unsigned:**reg
- **Signed**: Integer
```
4 bit unsigned: reg[3:0] var; // User defined size
signed: integer var; //32 bit

assume 
output [7:0] dout;
dout = var; // Automatically adjusts widths
```
### Simulation Datatypes
- **time**: 10ns (fixed)
- **realtime**: 10.13 ns (floats data type)
- **real:**: also floating point data type
- **Cannot be used in synthesis**
- We will need to add ip blocks to use floating point numbers in synthesis
## Blocking:
Blocking assignments are executed sequentially in the order they are written, meaning the variable on the left side is updated immediately before the simulator moves to the next statement. You should use blocking assignments exclusively when modeling combinational logic to ensure that intermediate signal changes propagate through the logic gates correctly within the same simulation time step.

## Non Blocking
Non-blocking assignments schedule their updates to occur at the end of the current time step, which allows the simulator to read the old values of all variables before any of them are updated. This behavior is essential for modeling sequential logic because it accurately mimics how hardware flip-flops capture data on a clock edge, preventing race conditions where the order of execution would otherwise change the outcome of your circuit.

## Reporting Mechanism
```
$display(); // $ indicates a system task
$monitor();
$strobe();
```
Each construct has a dedicated region in verilog.
### Active Region
- Blocking: LHS = xyz > executed in active region
- $display is executed in the active region
- Parameters
- Continuous assignments

### Postponed Regions
- Where monitor and strobe get executed

### Inactive Region
- Not really important?

### Non Blocking Assignment Region
- LHS <= xyz gets executed

### Others
- Preponed
- Observed 
- Reactive
These are only used SVA.

So:
- Use monitor when working esp. with non blocking assignments, as they will give updates better because using display with non blocking assignments will not give real time update as they are executed in different regions (active vs NBA). So NBA with display would show previous assignment value
- display should only be used in blocking assignments.
```
initial begin
#10;
$display(); // will show value at 10 ns
end

initial begin
#10
a <= 1
$display(); 
# 15;
a <= 0;// Here, it will NOT report 0. It will report 1
end
```
Print formats:
```
%0d // decimal
%0b // binary
%0o // octal
%0t // time
```
Code:
```
module tb;
 
// Declare a 4-bit register 'a' with an initial value of 0
reg [3:0] a = 4'h0;
 
 
initial begin
  a = 4'b1001; // Set 'a' to binary 1001
  #10; // Wait for 10 time units
  a = 4'b0001; // Set 'a' to binary 0001
  $display("Value of a_d : %0d @ %0t",a, $time); // Display the value of 'a' in decimal format, along with the current time
  #10; // Wait for 10 time units
  a = 4'b1010; // Set 'a' to binary 1010
  $display("Value of a_d : %0d @ %0t",a, $time); // Display the value of 'a' in decimal format, along with the current time
  #10; // Wait for 10 time units
  a = 4'b1010; // Set 'a' to binary 1010
  $display("Value of a_d : %0d @ %0t",a, $time); // Display the value of 'a' in decimal format, along with the current time
end
 
// Monitor the value of 'a' and display it along with the current time
initial begin
  $monitor("Value of a_m :%0d @ %0t", a, $time); // Display the value of 'a' in decimal format, along with the current time
end
 
endmodule
```

