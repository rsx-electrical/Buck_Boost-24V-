# Purpose of readme
This README describes each commit made to the `4_switch_Buck_Boost folder`. Add the most recent changes at the top, but below this "Purpose of readme" section.
Each commit section title in this README should follow this format: `Date, Name, Title of Commit`

## 02-27, Maria, High Side Switch
2N7002K: rsx nmos
BSS83P: rsx pmos only has Vds of 30V. rsx pmos is cutting it close because our vin can be 25ish. Dangerous if there are any spikes in our Vin. Chosen because it has a Vds of -60V which is very safe.
R106&R105: The Vgs of the pmos  (BSS83P) is +/- 20V. Having this voltage divide means that the gate of the pmos will be half the voltage of Vin. This will allow the pmos to turn on when required but have a Vgs range of 9V to 13V when the enable pin is on and it will be around 0 when the enable pin if off. These are all safe ranges.
### Next Steps
Find the spec for the LEDs that rsx has in stock. Find out what the the input voltage we will get from the microcontroller. Use this information to determine the exact values for the resistors at the gate of the nmos. 

### LTSpice Simulation
#### High Side Switch Vin is 25.6V
PMOS high-side switch LTSpice schematic with Vin of 25.6V

<img width="660" height="522" alt="image" src="https://github.com/user-attachments/assets/f6eb7d0f-f8cb-4af9-8605-7485536d42e9" />

When the enable input coming from a microcontroller (enable_vin) is set high, the enable pin (en_pin) on the LT8390 is set high. When the enable input is set low, the enable pin on the LT8390 is set low as well.

<img width="722" height="557" alt="image" src="https://github.com/user-attachments/assets/3887c24d-173d-4f97-891f-029ba7dfe583" />

The Vgs (Vpmos_gate - Vin) and Vds (Ven_pin - Vin) of the pmos. Vgs is safe within the maximum of +/- 20V. Vds is safe with a maximum of -60V. 

<img width="841" height="641" alt="image" src="https://github.com/user-attachments/assets/bf4269a3-e571-4a1f-94fb-6c91cf71c02c" />

The Vgs (Ven_pin) and Vds (Vnmos_drain) of the nmos. Vgs is safe within the maximum of +/- 20V. Vds is safe with a maximum of 60V. 

<img width="585" height="414" alt="image" src="https://github.com/user-attachments/assets/e7447e19-007e-42c2-ac80-56b83220556d" />

pmos Id is rated for -0.33A, nmos is rated for 320mA. Currents are in a safe range.

<img width="902" height="648" alt="image" src="https://github.com/user-attachments/assets/028c61a2-035d-4d36-b240-806db3dff240" />


#### High Side Switch Vin is 18V
PMOS high-side switch LTSpice schematic with Vin of 18V.

<img width="572" height="471" alt="image" src="https://github.com/user-attachments/assets/7d4bc736-6144-461c-95ce-192e8fe5c1af" />

When the enable input coming from a microcontroller (enable_vin) is set high, the enable pin (en_pin) on the LT8390 is set high. When the enable input is set low, the enable pin on the LT8390 is set low as well.

<img width="886" height="575" alt="image" src="https://github.com/user-attachments/assets/a16d71bb-35bd-4f5c-bce3-edcad9d4460b" />

The Vgs (Vpmos_gate - Vin), Vds (Ven_pin - Vin) and Id of the pmos. Vgs is safe within the maximum of +/- 20V. Vds is safe with a maximum of -60V. Id is safe as pmos is rated for -0.33A.

<img width="742" height="555" alt="image" src="https://github.com/user-attachments/assets/c83b3143-8a57-49a9-a9c6-513c7d98d193" />

The Vgs (Ven_pin) and Vds (Vnmos_drain) of the nmos. Vgs is safe within the maximum of +/- 20V. Vds is safe with a maximum of 60V. 

<img width="675" height="438" alt="image" src="https://github.com/user-attachments/assets/2d5a6f90-403f-45b3-bbd7-d55058e68d48" />

nmos current is good.

<img width="546" height="384" alt="image" src="https://github.com/user-attachments/assets/515ac98f-ea78-42e3-8d3c-10a535043e19" />








## 02-07, Maria, Reformat to be readable
Reformat to be split up into sections like the example Anthony gave us of a past boost converter. Input filtering capacitors with no values. They are placeholders. Values will need to be determined and number of capacitors will need to be determined. 

## 02-05, Maria, connected power path to chip
Yeah I know title doesn't make sense. Added power path (MOSFETTS and inductor) to schematic. Connected FB. Vout/Vfb = 24. Chosen resistance values are (232 + 10)/10 =24.2. The ratio is correct; however, I assume these values may be changes for resistors rsx has in storage. 603 resistors are used because low power will flow through them. Shunt resistors are used for current sensing. Again these may be replaces with resistance values for resistors we already have. The math for these values can be found in the Google doc. Capacitors for the BST1 and BST2 are 2.5uC because gate charge of MOSFETTs are 2.5e-8C and the capacitance should be 100x the gate charge. Things needed to be talked about: do we want to use shunt resistors, and what resistors do we have in stock to choose from. 

## 01-17, Anthony, added selection of res and caps
Basically just put in a couple of diff types of res and caps and their respective footprints (ceramic, polarized, shunt, basic shit that we'll prob use in the future, just pay attention to what each footprint corresponding to each symbol belongs to). 

603 and 805 usually for IC filtering with 805 for larger analog symbols (LDOs) and 1206 usually for bulk cap filtering of noise at input/outputs. Polarized caps used for stabilizing voltage/reducing ripple/storing energy/etc.

603 and res up usually depend on power dissipation, with the shunt being the widest and likely used for current sensing, if choose to go down this route into design, may need to change footprint, the Vishay one is overpowered and like for 0.0001ohm applications, which is, nah.
