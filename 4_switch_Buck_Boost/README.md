# Purpose of readme
This README describes each commit made to the `4_switch_Buck_Boost folder`. Add the most recent changes at the top, but below this "Purpose of readme" section.
Each commit section title in this README should follow this format: `Date, Name, Title of Commit`

## 03-05, Maria, Capacitors !!!
Thank you Anthony for the document about filtering ringing and ripple!!! The document helped with this section a lot. Also thank you to the LT890 data sheet for going through a bit about Cin and Cout capacitances. 
### Ringing Frequency
Ringing frequency of 75MHz-143MHz. 22nF will filter 30MHZ-100MHz range and 4.7nF will filter 100+MHz range. In a 4-switch buck-boost, the "Active Switching Side" moves depending on the mode (Buck or Boost). Therefore a  22 nF + 4.7 nF stack on required on both the Input and Output power rails to stay protected. At the high frequencies that ringing occurs at, the 15uH inductor between the two switching nodes is 2*pi*freq*(15e-6). For a frequency of 100MHz this comes to an impedance of 9.5KOhms. Maybe we can consider using snub circuits on the switching nodes? May not be required as power rails are protected.
### Bulk Capacitors
Calculations for the following are seen on this spreadsheet under the Capacitance Values tab: https://docs.google.com/spreadsheets/d/1GE4mJHaV0VTMqPT8AXjkSjW_NcW0vJ0DrAooZ-j17pU/edit?gid=2053012627#gid=2053012627
#### Cout
We want the output ripple to be at most 2 percent of the output voltage which is 0.480V. The output capacitence required to have this output ripple under boost conditions is at least  5.21uF and under buck conditions at least a 0.781uF output capacitance is required. To account for the Boost Right-Half-Plane Zero phenomenon a minimum of 57.9uF output capacitance is required.  To account for voltage undershoot an output capacitance of 1.46uF is required. Therefore for the circuit to be functional an output capacitance of at least 57.9uF is required. We want low ESR.  Two capacitances of 33uF can be used. 
#### Cin
A Cin of at least 1.14uF is required to maintain under a  input voltage ripple of 0.512V. However the input capacitance network should support a Irms current of Iout(max)/2 (see pg. 21 of LT8390 data sheet). No capacitor that small can support that large of a current. We also want a very small ESR. Therefore we should have larger capacitance values in parallel to split the current and lower ESR. For electrolytic capacitors that have smaller values their ESR is very large. Is it better to have only ceramic at the beginning. For now, I am going to put a placeholder value of three 22nF electrolytic capacitors or Cin. This will lower ESR and provide required capacitance. Ask this Saturday which type of capacitor would be best here. I feel like it would be ceramic. 
####Next Steps
Next steps would be determining the exact capacitors required. I am uncertain if we have capacitors in stock. Smth I will have to ask Anthony. 

## 02-27, Maria, High Side Switch
2N7002K: rsx nmos
BSS83P: rsx pmos only has Vds of 30V. rsx pmos is cutting it close because our vin can be 25ish. Dangerous if there are any spikes in our Vin. Chosen because it has a Vds of -60V which is very safe.
R106&R105: The Vgs of the pmos  (BSS83P) is +/- 20V. Having this voltage divide means that the gate of the pmos will be half the voltage of Vin. This will allow the pmos to turn on when required but have a Vgs range of 9V to 13V when the enable pin is on and it will be around 0 when the enable pin if off. These are aat least 1.46ll safe ranges.
### Next Steps
Find the spec for the LEDs that rsx has in stock. Find out what the input voltage we will get from the microcontroller. Use this information to determine the exact values for the resistors at the gate of the nmos. 

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
