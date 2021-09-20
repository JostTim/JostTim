# Hacking server fan speed control : 

Modifying the speed of server controlled fans to gain quietness.

________________

I use a second-hand racked server with a hardware RAID card to host a family file cloud system. (Owncloud v10, Ubuntu OS on a HP Proliant DL180 G6 server mounted with a 250GB RAID 0 on 2 drives (OS), and Data Storage on a 2To RAID 5 with 5 drives plus one automatic hotswap spare)



<img src="server.png" alt="IMG_20190223_163526" style="max-width:70%;" />

This is a professional high-end server, with ethernet management port and interface, as well as built in hardware RAID card, and is made available at very low prices because it has been in use in server houses for 10 years already. Accessing such high end robust hardware for light home usage is both convenient, and ecologically interesting, as it allows to continue using a still fully functional machines instead of disposing it.



The only issue with such professional equipment, comes from the fact that in data centers, the noise isn't an issue. In fact, server fans are "consumable" and are used at speeds that exceeds the real cooling needs, to prevent any failures. For the low computing power use that we make from this server at home, we don't need such noisy fans

Unfortunately, the fan speed in relation to temperature is controlled by the motherboard and isn't parametrable from the network management port interface. Similarly, disconnecting the fan or using more "classic ones" with no feedback triggers automatic power off of the server, to prevent failures.

Turning the server off if one fan breaks and stops turning is definitely a handy security feature, so, to keep the best and still reduce the noise, I used an Arduino as a "man in the middle", between fans and motherboard.

The fans uses open collector outputs to generate a PWM signal depending on the rotation speed, while another PWM signal is sent by the motherboard.

With an oscilloscope, I read the correspondence between the command PWM and the resulting feedback frequency that fans sent when executing the commands.

I used this as a "conversion function", and made the arduino able to send a command to the fan with a modulation factor between feedback and command, depending on user input, while maintaining a "fake answer" to the motherboard, to keep the built-in fan security system in a "peaceful" state.

By also reading of the actual answer of the fans with the arduino, I can detect if the fan turns to a complete stop, in case of a fatal failure for example, and in such a condition, update the fake answer to the motherboard to a flat signal, to trigger the soft power off of the server via the built-in fan speed security system.