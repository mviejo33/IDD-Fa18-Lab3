# Data Logger (and using cool sensors!)

*A lab report by Manuel Viejo.*

For this lab, we will be experimenting with a variety of sensors, sending the data to the Arduino serial monitor, writing data to the EEPROM of the Arduino, and then playing the data back.

## Part A.  Writing to the Serial Monitor
 
**a. Based on the readings from the serial monitor, what is the range of the analog values being read?**
 
 0-1023
 
**b. How many bits of resolution does the analog to digital converter (ADC) on the Arduino have?**

10

## Part B. RGB LED

**How might you use this with only the parts in your kit? Show us your solution.**

## Part C. Voltage Varying Sensors 
 
### 1. FSR, Flex Sensor, Photo cell, Softpot

**a. What voltage values do you see from your force sensor?**

0-1000 approximately 

**b. What kind of relationship does the voltage have as a function of the force applied? (e.g., linear?)**

Not linear, by applying little force it jumps up to high values 700~ and then it gets harder to increment.

**c. In Examples->Basic->Fading the LED values range from 0-255. What do you have to do so that you get the full range of output voltages from the LED when using your FSR to change the LED color?**

Use the map function to map the values from 0-1000 aproximately to 0-255

**d. What resistance do you need to have in series to get a reasonable range of voltages from each sensor?**

Using the 10KOHM resistance with the map function will allow me to have the necessary ranges from each sensor.

**e. What kind of relationship does the resistance have as a function of stimulus? (e.g., linear?)**

Not really linear, its a log graph, at especially low force measurements it quickly goes from infinite to 100 KOHM.

### 2. Accelerometer
 
**a. Include your accelerometer read-out code in your write-up.**

Values on the left were already normalized for LED

![Image of accelerometer_readings](https://github.com/mviejo33/IDD-Fa18-Lab3/blob/master/accel_readings.PNG)

### 3. IR Proximity Sensor

**a. Describe the voltage change over the sensing range of the sensor. A sketch of voltage vs. distance would work also. Does it match up with what you expect from the datasheet?**

It is not linear, the rate at which it increments gets bigger if I my finger is very close to it. 

**b. Upload your merged code to your lab report repository and link to it here.**

I added the proximity sensor's reading on top of the readings that I had from the accelerometer-LCD file

## Optional. Graphic Display

**Take a picture of your screen working insert it here!**

## Part D. Logging values to the EEPROM and reading them back
 
### 1. Reading and writing values to the Arduino EEPROM

**a. Does it matter what actions are assigned to which state? Why?**

Yes, there are states that erase/add/modify memory, it depends on what you want to do. You dont want to erase memory that is not there, you dont want to add memory blocks when it's already full.

**b. Why is the code here all in the setup() functions and not in the loop() functions?**

Because its already being looped in the main file, we just need it to execute that code one time once a state is changed.

**c. How many byte-sized data samples can you store on the Atmega328?**

1024

**d. How would you get analog data from the Arduino analog pins to be byte-sized? How about analog data from the I2C devices?**

The arduino digitalRead() function outputs integer values between 0 and 1023, by using the map function I can normalize these values to some value between 0 and 255. Same will be true for the output of the I2C devices but with a different min and max.

**e. Alternately, how would we store the data if it were bigger than a byte? (hint: take a look at the [EEPROMPut](https://www.arduino.cc/en/Reference/EEPROMPut) example)**

Consume the whole byte and then move the address to the next byte and then save the rest of the object with the put method

**Upload your modified code that takes in analog values from your sensors and prints them back out to the Arduino Serial Monitor.**

[Code](https://github.com/mviejo33/IDD-Fa18-Lab3/blob/master/accel_proximity_I2C.ino)

### 2. Design your logger

![PDF_diagram](https://github.com/mviejo33/IDD-Fa18-Lab3/blob/master/diagram_lab3.pdf)

### 3. Create your data logger!
 
**a. Record and upload a short demo video of your logger in action.**

Step counter

https://www.youtube.com/watch?v=8EVRrnQS09k
