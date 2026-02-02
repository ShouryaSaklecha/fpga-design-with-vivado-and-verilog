# Vivado Gui Notes


## Schematic Tooling
Clicking RTL Analysis > Open Elaborated Design > Schematic allows to use:
1. See the gate level logic of verilog.
2. See the LUT to Logic mapping.

In tb, you can use:
1. force clock: create a signal to be a clock.
2. force signal: set a signal 1 or 0 as needed.

### Leaf Cells
In Vivado, a leaf cell represents the most fundamental unit of hardware logic that cannot be subdivided further within the design hierarchy. It is a primitive component that maps directly to the physical resources of the FPGA fabric such as look-up tables, flip-flops, or digital signal processing slices. These cells act as the functional building blocks where actual logic operations occur or where data is stored. Because they are at the bottom of the design tree, you can constrain their specific physical location on the chip, but you cannot look inside them for more granular logic modules.
### Nets
A net is the logical representation of a signal path that provides electrical connectivity between the pins of different cells. It functions as the virtual wire that carries data or clock signals from a single driver, such as an output pin of a flip-flop, to one or more loads, such as the input pins of a look-up table. In the Vivado database, nets are the objects used to analyze routing delays and congestion, as they define how signals navigate the FPGA interconnect fabric to link the various logic components together.

## Synthesis Tooling
Ensure TB code is under "simulation" and design under "Design Sources".

### Clocks and XDC
You should search for "master" xdc files by searching on google based on your board. The XDC files:
1. Have default clocking information.
2. Have some/or all, basic IO mapping.
