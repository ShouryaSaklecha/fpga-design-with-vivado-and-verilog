# Modelling Styles
## Types
- Gate Level
- Switch Level (NOT synthesizable)
- Structural Modelling 
- Behavioural Modelling

## Assignment Operators
in any operator, the system is:
```
LHS <operator> RHS
```
### Procedural
- If we have reg on the LHS
- RHS can be anything
### Continuous
- If we have wire/net on the LHS
- RHS can be anything

## What Differs?
Consider a code block:
```
// Continuous
assign y = a & b & c;

// Procedural
reg y;
always @ ()
begin
y = a & b & c;
end
```
- procedural will need an always block. 
- If a, b or c changes in continuous, it gets revaluated immediately.
- In procedural, it gets revaluated based on what is in the sensitivity list. When that changes, revaluated.

## Example: Swapping in Blocking vs NB
- For Blocking Assignments, evaluation and value updation both happen in Active Region.
- For NB, evaluation takes place in active region and updation takes place in NB region.
```
a = 3
b = 6

// In blocking:
a = b; // will work
b = a; // b will be b because a was b before.

// So we need
tmp = a; 
a = b;
b = temp;

// In NB, this works because they execute with old values, and only get updated later.
a <= b; a will be 6;
b <= a; b will be 3;
```





