# Potter's Wheel : 

Homemade wood electrical potter's wheel with adjustable speed, with a "recycled" motor.

_____________

Starting with a cheap table potter's ["tournette"](https://loisir-creatif-fr.buttinette.com/shop/a/tournette-de-potier-11-x-18-cm-51128), I modeled an enclosure in thick plywood, with apertures to convenientely clean excess water and mud after clay work.

<img src="steps.png" alt="steps" style="max-width:80%;" />

To motorize the wheel I decided to use an old asynchronous 220 V motor from a disposed blender. The motor is running without load at 3600 rpm. I found that most potters wheel range up to 200 rpm. 

The reduction ratio for the belts and pulleys should then be about 18:1, at idle rotation.

Using small pulleys at the common format GT2 and printing the other ones to match the given ratio, I obtained the load transmission assembly.

<img src="Motorization.png" alt="Motorization" style="max-width:50%;" />

<img src="photo_box.png" alt="photo_box" style="max-width:40%;" />

Once the whole building was complete, it was time to make the wheel speed driveable by a user.

To control an asynchronous motor speed, a possible & easy solution is to use Triacs and Phase detectors, to allow current to pass inside the motor in phase with the 50Hz oscillation of the grid. The goal is to delay more or less from the 0V point of the AC current, the point at which we start letting current pass in the motor, depending on how much energy we want to inject in it.

The energy received by the motor over time is then related to the area under the curve (in yellow in the graph below), from the timing at which we pull the "trigger" of the triac, to the next 0V point, at which the triac resets itself and cuts open the 220V circuit to the motor.



 <img src="Triac220V_driving.png" alt="Triac220V_driving" style="max-width:70%;" />

The measure of the phase of the 220V is done with an optocoupler linked to a microcontroller. (optocouplers are usually used when one wants to transmit signals from high voltage components to logic levels or reciprocally. They secure the material, as the signal is sent with light from a high voltage LED to a low voltage photodetector, thus the low and high voltage areas never meet.)

Finally, the microcontroller simply receives analog inputs from a potentiometer or a pedal (in which sits a linear variable resistance), and controls the duration of the Δoff epoch based on the potentiometer value.