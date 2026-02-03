# Fundamentals Part 2
## Operators
### Arithematic
Basically same as other languages 
```
reg [3:0] din1 = 4'd5, din2 = 4'd6;

// Arithmetic Operators
add = din1 + din2; // 11
sub = din1 - din2; // 15 since it is unsigned we cant have negatives
mul = din1 * din2; // 14 because 30 does not sit in the datatype, so display has truncated it.

// if we use
integer sub;
reg [7:0] mul;
// They both will work

// LOGICAL: 
~a; // NOT
a & b; // AND
a | b; // OR
a ^ b; // XOR

// Shift
a >> b; // right shift
a << b; // Left Shift

// Concat
reg [8:0] din3 = {din1,din2};
// Repetition
reg [8:0] din3 = {2{din1}}; // 2 din1's

// Ternary
() ? a : b;
```
