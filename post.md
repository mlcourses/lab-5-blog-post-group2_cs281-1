# Lab 5: Finite State Machine Design

# Overview and Motivation
Welcome to Lab 5 of CS281: Introduction to Computer Systems! <br>
In this lab we will build a circuit that reads a binary number and determines if that input is divisible by 3. 
We'll explore how to connect these components with an idea of DFA and JK flip flop.

# Objectives of the Lab
1.  This lab is to design a circuit that reads a binary number input one bit at a time and determines whether the binary number represented by the input is divisible by 3.
   
# Materials
- PB-503 Breadboard prototyping station (an integrated device with a number of electrical components like switches)
- Wires
- Multimeter 
- Resistors
- JK Flip-Flops
- Logic Gates (AND, OR, NOT)
- Computer with Arduino IDE installed

# Overview: 

1. Circuit Design: The binary number will be fed to the circuit, one bit at a time, starting with the highest order bit and ending with
the lowest order bit. Each bit will be clocked into the circuit using a separate clock input.
<br><img width="770" height="500" src="lab_f2.png">






<br><img width="600" height="500" src="lab_f1.png">









# Circuit Design: 
## 1. Build a Finite State Machine (DFA)


We began by constructing a Finite State Machine (FSM) using a state transition diagram. 
The FSM depicts the various states the circuit can be in and the transitions between them based on the input bits. <br>

<br><img width="600" height="500" src="lab53.jpeg">


## 2. Boolean Truth Table

Build truth table for the J and K inputs of each flip-flop and the output of the circuit.
The outputs of your truth table are the J and K values for each flip flop in your memory portion of the
circuit. You will also have an output for out, the overall circuit output.

<br><img width="750" height="500" src="lab51.jpeg">


#### Note: Remember to include don’t cares whenever possible because they greatly ease the circuit design in the next

## 3. Create K-Maps

Using the Boolean Truth Table, create K-Maps and minimized the logical expressions to simplified equations.
<br><img width="600" height="500" src="lab52.jpeg">


## 4. Build the circuit in logisim

Built the circuit in Logisim and test it is working as expacted.

https://github.com/AdvancedUno/lab-5-blog-post-group2_cs281-1/assets/108073642/25083ae7-0a83-4122-8dc2-e3a05703fd09



## 5. Build the circuit on the breadboard
### Building:
1. Wire the clock to one push button. Wire it so that button in the unpressed state is low and the button
pressed is high.
2. Wire the input bit (x) to the other push button. Wire it so that button in the unpressed state is low and the
button pressed is high.
3. Wire values Q1 and Q0 to logic probes 1 and 0 (or 2 and 1). That way we can always see the current
state.


<div style="display: flex; justify-content: center;">
    <img width="650" height="500" src="IMG_0463.JPG" alt="">
</div>


5. Wire output to the last logic probe.
6. Make use of the CLEAR feature for the FFs so that you can reset the circuit back to the start state
asynchronously.
7. Be sure to read the spec sheet for the JK flip flop very carefully. You will find some additional inputs on
the real JK IC that do not appear on the simplified logisim model

<br><img width="750" height="500" src="IMG_04641.JPG">
<br>

### Testing:

https://github.com/AdvancedUno/lab-5-blog-post-group2_cs281-1/assets/108073642/590413de-dfee-4612-b595-be562c99fcab



<br>
<br>







# Conclusion

This lab allowed us to get a deeper understanding of sensors and actuators such as buzzers and ultrasonic sensors.
By using an Arduino device and circuit, we created tools that may have practical use in our daily lives instead of just wiring circuits and testing. For the last component of the lab, we practiced how to combine two or more devices and tools to create more complex and useful devices that can be good practice for future labs and even for future careers. 













