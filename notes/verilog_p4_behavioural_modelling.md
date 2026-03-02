# Behaviour Modelling Style

## Typical Skeleton
- Need to use an always block, and potentially an initial begin
- Use reg types

### Declare Module
- Ports
- Temprary variables

### Initial Begin
We need to initialise ALL declared variables so reg should be here. 

### Always Block
- Make sure LHS is a reg type
- Can use blocking operator "=" here.

### Post Always: ASSIGN 
use assign to assign a value on the port variable. 

## Constructs

### Initial
Used to declare only the first state of values.
### Always
Fundamental construct for behavioral modelling. 
- Combinational Circuit: Output depends on all inputs.
- Sequential Circuit: Output depends on the FASTEST signal, almost always the clock. 
  
Let's see a COMBINATIONAL 3 input AND gate with inputs a, b, c
```
always@(a,b,c) // Or use always@(*)
```
SEQUENTIAL CIRCUIT
```
always@(posedge clk) // Sensitive on + edge of clock
always@(negedge clk) // Sensitive on -ve edge
```
