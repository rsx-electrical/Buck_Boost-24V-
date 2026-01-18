# Purpose of readme
This README describes each commit made to the `4_switch_Buck_Boost folder`. Add the most recent changes at the top, but below this "Purpose of readme" section.
Each commit section title in this README should follow this format: `Date, Name, Title of Commit`

'01-17, Anthony, added selection of res and caps'
Basically just put in a couple of diff types of res and caps and their respective footprints (ceramic, polarized, shunt, basic shit that we'll prob use in the future, just pay attention to what each footprint corresponding to each symbol belongs to). 

603 and 805 usually for IC filtering with 805 for larger analog symbols (LDOs) and 1206 usually for bulk cap filtering of noise at input/outputs. Polarized caps used for stabilizing voltage/reducing ripple/storing energy/etc.

603 and res up usually depend on power dissipation, with the shunt being the widest and likely used for current sensing, if choose to go down this route into design, may need to change footprint, the Vishay one is overpowered and like for 0.0001ohm applications, which is, nah.