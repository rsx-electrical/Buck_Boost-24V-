# Inverting Buck Practice
Inverting Buck Board using MC33063AD topology for Inverting Regualtors (3V --> -2V)

First Iteration:
<img width="1352" height="666" alt="OldMariaInvertBuck" src="https://github.com/user-attachments/assets/e0bc18ff-d663-49ae-ab87-18a4a92cb7d2" />

Made a couple of changes, aligned the gnd and vout terminals of the screw terminal and capacitor so at to have a cleaner and wider vout/gnd copper pour, with buck having a larger Iout>Iin, so less power less internally with potetnually larger current.

Also went ahead and drew all the passive components for the IC as closer to the main body of the chip as possible, this will come into greater importance later on when working with more complicated PWM controllers, espcially with analog traces, having as close of a connection for traces conducting in the mA order succombing to greater loss the longer the distance it has to travel to communicate with the IC.

Via placemnt centralized at the capacitor (input and output, with discharge into ground requiring the greatest degree of stitching with a return path to the bottom ground layer.

Edited Second Iteration:
<img width="1502" height="773" alt="image" src="https://github.com/user-attachments/assets/e6002c8c-ffe7-48f5-8ddf-6b1e6790d39b" />

Tried to make the board as tight and small as possible, the modified version is not the 'best' version. You don't hvae to make additional edits, but if you chose to you absolutely can, but regardless, where do you think the board can be improved and why? If you're not sure if there can be improvements, or feel unsure to the 'why?' part of the question, please let me know on the discord. 
