# Purpose of readme
This README describes each commit made to the `4_switch_Buck_Boost folder`. Add the most recent changes at the top, but below this "Purpose of readme" section.
Each commit section title in this README should follow this format: `Date, Name, Title of Commit`
## 02-05, Maria, connected power path to chip
Yeah I know title doesn't make sense. Added power path (MOSFETTS and inductor) to schematic. Connected FB. Vout/Vfb = 24. Chosen resistance values are (232 + 10)/10 =24.2. The ratio is correct; however, I assume these values may be changes for resistors rsx has in storage. 603 resistors are used because low power will flow through them. Shunt resistors are used for current sensing. Again these may be replaces with resistance values for resistors we already have. The math for these values can be found in the Google doc. Capacitors for the BST1 and BST2 are 2.5uC because gate charge of MOSFETTs are 2.5e-8C and the capacitance should be 100x the gate charge. Things needed to be talked about: do we want to use shunt resistors, and what resistors do we have in stock to choose from. 

## 01-17, Anthony, added selection of res and caps
Basically just put in a couple of diff types of res and caps and their respective footprints (ceramic, polarized, shunt, basic shit that we'll prob use in the future, just pay attention to what each footprint corresponding to each symbol belongs to). 

603 and 805 usually for IC filtering with 805 for larger analog symbols (LDOs) and 1206 usually for bulk cap filtering of noise at input/outputs. Polarized caps used for stabilizing voltage/reducing ripple/storing energy/etc.

603 and res up usually depend on power dissipation, with the shunt being the widest and likely used for current sensing, if choose to go down this route into design, may need to change footprint, the Vishay one is overpowered and like for 0.0001ohm applications, which is, nah.
