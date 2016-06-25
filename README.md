# Car Controller
This project provides firmware that runs on an arduino.  This firmware, coupled with an arduino, provides a serial (UART) interface for outputting PWM signals.  Something like a raspberry pi has lots of processing power and I/O; but it can't reliably drive PWM outputs for servos etc.  Due to the PWM being done in software, any slight lag will effect the precise timing required.

By sending the steering and motor outputs over UART to a real time microcontroller, reliability can be ensured.  This is because these microcontrollers are specifically designed for stuff like this with very precise timing.  The firmware also reports the voltage of a battery; which is great for remote monitoring and safety.

## Setup
It's fairly straight forward to use.  The PWM output and voltage monitoring pins are in configurable variables at the start of the program.  Specify which pins you're using; bear in mind the voltage monitor must be an analog input.  

### Voltage Monitoring
If the maximum voltage of the battery is less than your microcontroller's operating voltage no extra hardware is needed.  Just splice a wire into where you want to measure and connect it to the arduino's pin.  For LiPo and other multi cell batteries, it is generally only necessary to monitor a single cell.  Simply tap into the first cell on the balance connector.

### Steering/Motor Driver
#### Steering
The steering pin will output a PWM signal using Ardiuno's built in servo library.  It will drive practically any servo.

#### Motor Controller
The motor controller pin will out a PWM signal using Arduino's normal analogWrite() function.  This *will not* drive most standard ESCs (speed controllers).  It will work on drivers like [pololu's 18v7] (https://www.pololu.com/product/2991).  If anyone wants to drive an ESC just open an issue and I'll add it in.

# Usage
You can send it three commands via UART, "motor,x" to control motor output (0-255), "steer,x" to control steering output (useful steering normally about 50-150) and "motor-dir,x" (x is 0 or 1) for the motor direction pin.  car-controller will print the current battery voltage at 2Hz.  If the debug flag is set to true when uploaded, it sends messages to the serial console every time you change an ouput.

# License
As with all my projects this is released under a GNU GPLv3 or later license in the hope it will be useful.
