# Arduino_Reaction_Game
A game that tests your reaction time using an Arduino uno, two LEDs, two resistors and a button.

This was one of my first hands-on Arduino projects. The basic idea came from an Arduino project book, but I designed and built the circuit myself and wrote and adapted the code to make the game work.

## How it works:

The game uses two LEDs:

🟢 Green LED — waiting for the reaction
🔴 Red LED — indicates the other state

After a random amount of time, the green LED turns on and the red LED turns off. The player then has to press the button as quickly as possible.

The waiting time is randomized, so the player cannot predict when the signal will change. The reaction time is measured using the Arduino's millis() function and displayed in the Serial Monitor.

For example:

Your reaction time is: 0.32 seconds.

The random delay can vary significantly, meaning the light can change relatively quickly or take several seconds.

### Hardware
Arduino Uno
1 × push button
1 × green LED
1 × red LED
2 × resistors
Breadboard
Jumper wires
Circuit




The button is connected using the Arduino's internal pull-up resistor:

pinMode(buttonPin, INPUT_PULLUP);

The two LEDs are connected to digital pins 12 and 13.

Program structure

The program can roughly be divided into three parts:

### 1. Waiting for the light change

A random delay is generated using:

randomSeed(analogRead(0));

and:

int randNumb = random(10000);
delay(randNumb);

This makes the timing unpredictable for the player.

### 2. Measuring reaction time

When the reaction light is activated, the program stores the current time:

timePassed = millis();

When the button is pressed, the elapsed time is calculated:

reactionTime = millis() - y;

The result is then converted to seconds and printed to the Serial Monitor.

### 3. Button debouncing

One of the more challenging parts of the project was getting the button input to behave reliably.

Mechanical buttons can produce several very rapid electrical transitions when pressed. This can cause the Arduino to interpret one press as multiple presses.

I therefore implemented a debounce function using a short delay period:

unsigned long debounceDelay = 50;

The function checks whether the button state has remained stable before accepting the new state.

This was one of the concepts I learned while working on this project and helped me understand that physical hardware does not always behave as simply as the code might suggest.

### What I found challenging

The most difficult parts of this project were:

designing the circuit correctly
understanding how the different states of the LEDs should work
figuring out the program logic
measuring the reaction time correctly
getting the button input to work reliably
understanding and implementing debouncing

The project was particularly useful because I had to connect the programming logic to what was physically happening in the circuit.

### What I learned

Through this project I learned about:

digital inputs and outputs
LEDs and resistors
Arduino Uno
INPUT_PULLUP
functions
variables and program states
random numbers
millis() and measuring elapsed time
Serial communication
button debouncing
debugging both hardware and software

Most importantly, I learned that building an embedded system involves thinking about both the physical circuit and the software controlling it.

### Project origin

The basic reaction-game idea was taken from an Arduino project book.

I did not design the original concept, but I built the circuit myself, implemented the program, worked out the program logic, and experimented with the implementation.

### Possible improvements

There are several things I would like to improve in a future version:

Add a display instead of using the Serial Monitor
Keep track of the fastest reaction time
Add multiple rounds and calculate an average reaction time
Add a start/reset button
Improve the game logic so the player cannot press the button before the signal
Create a more compact version of the circuit
Design a PCB instead of using a breadboard

### Project sttatus

Completed — first Arduino/embedded electronics project

Technologies: Arduino · C/C++ · Electronics · Embedded Systems
